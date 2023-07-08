<div align="center">
  <a href="https://github.com/Nerdware-LLC">
    <img src="https://github.com/Nerdware-LLC/.github/blob/main/profile/nerdware_logo.png" height="120" alt="Nerdware_Logo" />
  </a>
  <h1>Reusable GitHub Actions Workflows</h1>

Author: [Trevor Anderson](https://github.com/trevor-anderson), Founder of [Nerdware](https://github.com/Nerdware-LLC)

</div>

- 🚀 Available Workflows:
  - [ECR Image Push](#ecr-image-push)
  - [Get Docker Tags](#get-docker-tags)
  - [Node Test](#node-test)
  - [S3 Image Upload](#s3-image-upload)
  - [Semantic Release](#semantic-release)
  - [Upload to S3](#upload-to-s3)
- [📖 Relevant GitHub Documentation](#-relevant-github-documentation)
- [📝 License](#-license)
- [💬 Contact](#-contact)

---

## [ECR Image Push](/.github/workflows/ecr_image_push.yaml)

This workflow builds a Docker image using [BuildKit](https://github.com/moby/buildkit) and uploads it to an ECR repo.

**Requirements:**

- You must have an existing ECR image repo.
- The calling workflow must specify an [OpenID Connect IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html) ARN with which the relevant API calls can be authenticated. Support for other forms of authentication may be added in the future.

**Usage:**

```yaml
jobs:
  my_job_using_ecr_image_push:
    uses: Nerdware-LLC/reusable-action-workflows/.github/workflows/ecr_image_push.yaml@v1.3.0 # or "@main"
    secrets:
      OIDC_GITHUB_ROLE_ARN: ${{ secrets.OIDC_GITHUB_ROLE_ARN }}
      AWS_ECR_PRIVATE_REPO: ${{ secrets.AWS_ECR_PRIVATE_REPO }}
      AWS_ECR_REGION: ${{ secrets.AWS_ECR_REGION }}
    permissions:
      id-token: write
      contents: read
```

## [Get Docker Tags](/.github/workflows/get_docker_tags.yaml)

This workflow outputs a JSON-formatted array of three Docker tags which can be used in `docker build` and/or `docker tag` commands.

In order, the tags provided in the output are as follows:

1. "latest", a constant which this action always includes in the output.
2. A version tag based either on the version-tag input OR the "version" property in a package.json, if one is present.
3. A ref tag based on the variable component of the GITHUB_REF env var, the value of which depends on the type of event which triggered the Action run:

   | EVENT        | REF                           | IMAGE TAG       |
   | :----------- | :---------------------------- | :-------------- |
   | branch push  | `refs/heads/<branch_name>`    | `<branch_name>` |
   | pull request | `refs/pull/<pr_number>/merge` | `<pr_number>`   |
   | release      | `refs/tags/<release_tag>`     | `<release_tag>` |

**Usage:**

```yaml
jobs:
  my_job_using_get_docker_tags:
    uses: Nerdware-LLC/reusable-action-workflows/.github/workflows/get_docker_tags.yaml@v1.3.0 # or "@main"
    with:
      tag-prefix: my-image-name # required input
      version-tag: v1.0.0 # optional input - defaults to the "version" specified in package.json
```

## [Node Test](/.github/workflows/node_test.yaml)

This workflow sets up NodeJS, runs your `test-script` (default: `test:ci`), updates the GitHub commit status, and optionally updates [CodeCov](https://about.codecov.io/). The input `env-vars` is a string formatted as a space-separated list of environment variables to be set in the workflow; this is a workaround to the limitation that [the `env` context in caller workflows is not propagated to called workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows#limitations). The input `test-script` is the name of the npm script to run.

**Artifacts:**
If your `test-script` creates coverage reports at `<repo-root>/coverage`, the coverage dir will be uploaded as an artifact named `coverage-reports`. This artifact can be downloaded in a subsequent step using the [download-artifact](https://github.com/actions/download-artifact) action. To disable this behavior, set the input `should-upload-coverage-artifacts` to `false`.

**Usage:**

```yaml
jobs:
  my_job_using_node_test:
    uses: Nerdware-LLC/reusable-action-workflows/.github/workflows/node_test.yaml@v1.3.0 # or "@main"
    with:
      test-script: "test:ci"
      # Note the >- below; this block-chomping indicator will rm all newline chars, and separate each line by a space.
      env-vars: >-
        MY_ENV_VAR=my-env-var-value
        FOO=bar
        BAZ=qux
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }} # <-- Optional
```

## [S3 Image Upload](/.github/workflows/s3_image_upload.yaml)

This workflow builds a Docker image as a ZIP archive and then uploads it to an S3 bucket.

**Requirements:**

- You must have an existing S3 bucket with [_default SSE encryption_](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-encryption.html). Support for buckets encrypted with a user-managed KMS key may be added in the future.
- The calling workflow must specify an [OpenID Connect IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html) ARN with which the relevant API calls can be authenticated. Support for other forms of authentication may be added in the future.

**Usage:**

```yaml
jobs:
  my_job_using_s3_image_upload:
    uses: Nerdware-LLC/reusable-action-workflows/.github/workflows/s3_image_upload.yaml@v1.3.0 # or "@main"
    with:
      image-name: foo-image-name
    secrets:
      OIDC_GITHUB_ROLE_ARN: ${{ secrets.OIDC_GITHUB_ROLE_ARN }}
      S3_BUCKET_DEST: ${{ secrets.S3_BUCKET_DEST }}
      S3_BUCKET_REGION: ${{ secrets.S3_BUCKET_REGION }}
```

## [Semantic Release](/.github/workflows/release.yaml)

This workflow uses [Semantic Release](https://github.com/semantic-release/semantic-release) to publish a GitHub release.

**Requirements:**

- Configuration: Your repo must include a [Semantic Release config file](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/configuration.md#configuration).
- Authentication: You must provide an auth token granting push access to the project Git repo via a secret named `SEMANTIC_RELEASE_TOKEN`. [Semantic Release requires these permissions in order to create git tags](https://github.com/semantic-release/semantic-release/blob/master/docs/usage/ci-configuration.md#authentication).
  - If your repo _does not_ use [branch protection rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches), the default `$GITHUB_TOKEN` is sufficient.
  - If your repo _does_ include branch protection rules, the calling workflow must instead provide a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) granting push access to the project Git repo.

**Usage:**

```yaml
jobs:
  my_job_using_release:
    uses: Nerdware-LLC/reusable-action-workflows/.github/workflows/release.yaml@v1.3.0 # or "@main"
    secrets:
      SEMANTIC_RELEASE_TOKEN: ${{ secrets.SEMANTIC_RELEASE_TOKEN }} # or $GITHUB_TOKEN (see above requirements)
```

## [Upload to S3](/.github/workflows/upload_to_s3.yaml)

This workflow creates a NodeJS build via `npm run build`, and then uploads the resultant package to an S3 bucket using the [`aws s3 sync`](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/sync.html) command.

**Requirements:**

- Your project's repo root must include a `package.json` file with a defined `build` script.
- You must have an existing S3 bucket with [_default SSE encryption_](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-encryption.html). Support for buckets encrypted with a user-managed KMS key may be added in the future.
- The calling workflow must specify an [OpenID Connect IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html) ARN with which the relevant API calls can be authenticated. Support for other forms of authentication may be added in the future.

**Usage:**

```yaml
jobs:
  my_job_using_upload_to_s3:
    uses: Nerdware-LLC/reusable-action-workflows/.github/workflows/upload_to_s3.yaml@v1.3.0 # or "@main"
    with:
      s3-sync-command-params: "--acl bucket-owner-full-control --sse AES256"
      # The above s3-sync command params would be sufficient for a bucket with default SSE encryption
      # and standard ACL protections. For more info on s3-sync command options, see the documentation
      # at https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/sync.html#options
    secrets:
      OIDC_GITHUB_ROLE_ARN: ${{ secrets.OIDC_GITHUB_ROLE_ARN }}
      S3_BUCKET_REGION: ${{ secrets.S3_BUCKET_REGION }}
      S3_UPLOAD_PATH: ${{ secrets.S3_UPLOAD_PATH }} # my_foo_bucket/production
```

---

### 📖 Relevant GitHub Documentation

- https://docs.github.com/en/actions/using-workflows/reusing-workflows

## 📝 License

Nerdware-LLC/reusable-action-workflows is licensed under the [`Apache License 2.0`](/LICENSE), a permissive license whose main conditions require preservation of copyright and license notices. Contributors provide an express grant of patent rights. Licensed works, modifications, and larger works may be distributed under different terms and without source code.

See [LICENSE](/LICENSE) for more information.

<div align="center" style="margin-top:35px;">

## 💬 Contact

Trevor Anderson - [@TeeRevTweets](https://twitter.com/teerevtweets) - [Trevor@Nerdware.cloud](mailto:Trevor@Nerdware.cloud)

  <a href="https://www.youtube.com/channel/UCguSCK_j1obMVXvv-DUS3ng">
    <img src="./.github/assets/YouTube_icon_circle.svg" height="40" />
  </a>
  &nbsp;
  <a href="https://www.linkedin.com/in/trevor-anderson-3a3b0392/">
    <img src="./.github/assets/LinkedIn_icon_circle.svg" height="40" />
  </a>
  &nbsp;
  <a href="https://twitter.com/TeeRevTweets">
    <img src="./.github/assets/Twitter_icon_circle.svg" height="40" />
  </a>
  &nbsp;
  <a href="mailto:Trevor@Nerdware.cloud">
    <img src="./.github/assets/email_icon_circle.svg" height="40" />
  </a>
  <br><br>

  <a href="https://daremightythings.co/">
    <strong><i>Dare Mighty Things.</i></strong>
  </a>

</div>

<!-- LINKS -->

[pre-commit-shield]: https://img.shields.io/badge/pre--commit-33A532.svg?logo=pre-commit&logoColor=F8B424&labelColor=gray
[semantic-shield]: https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-E10079.svg
[semantic-gh-action-url]: https://github.com/cycjimmy/semantic-release-action
[license-shield]: https://img.shields.io/badge/license-Proprietary-000080.svg?labelColor=gray
[gh-action-docs-url]: https://docs.github.com/en/actions/security-guides/encrypted-secrets
[gh-pat-docs-url]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
