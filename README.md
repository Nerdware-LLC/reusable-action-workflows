<br>
<div align="center">

  <a href="https://github.com/Nerdware-LLC">
    <img src="https://github.com/Nerdware-LLC/.github/blob/main/profile/nerdware_logo.png" height="120" alt="Nerdware_Logo" />
  </a>

  <h1>Reusable GitHub Actions Workflows</h1>

Author: [Trevor Anderson](https://github.com/trevor-anderson), Founder of [Nerdware](https://github.com/Nerdware-LLC)

</div>

- [🚀 Available Workflows](#-available-workflows)
  - [ECR Image Push](#ecr-image-push)
  - [Get Docker Tags](#get-docker-tags)
  - [Run Jest Tests](#run-jest-tests)
  - [S3 Image Upload](#s3-image-upload)
  - [Semantic Release](#semantic-release)
- [📖 Relevant GitHub Documentation](#-relevant-github-documentation)
- [📝 License](#-license)
- [💬 Contact](#-contact)

## 🚀 Available Workflows

### ECR Image Push

<div style="padding-left:20px;">

[ecr_image_push.yaml](/.github/workflows/ecr_image_push.yaml) <br>
This Workflow builds a Docker image and uploads it to an ECR repo.

</div>

### Get Docker Tags

<div style="padding-left:20px;">

[get_docker_tags.yaml](/.github/workflows/get_docker_tags.yaml) <br>
This Workflow outputs a JSON-formatted array of Docker tags which can be used in `docker build` and/or `docker tag` commands.

Provided Tags:

1. "latest", a constant which this action always includes in the output.
2. A "version" tag based either on the version-tag input OR the "version" property in a package.json, if one is present.
3. A "ref" tag based on the variable component of the GITHUB_REF env var, the value of which depends on the type of event which triggered the Action run:

   | EVENT        | REF                           | IMAGE TAG       |
   | :----------- | :---------------------------- | :-------------- |
   | branch push  | `refs/heads/<branch_name>`    | `<branch_name>` |
   | pull request | `refs/pull/<pr_number>/merge` | `<pr_number>`   |
   | release      | `refs/tags/<release_tag>`     | `<release_tag>` |

</div>

### Run Jest Tests

<div style="padding-left:20px;">

[jest_test.yaml](/.github/workflows/jest_test.yaml) <br>
This Workflow runs Jest tests and optionally updates Codecov.

> An npm script named `test:ci` must be present in the `package.json`.

</div>

### S3 Image Upload

<div style="padding-left:20px;">

[s3_image_upload.yaml](/.github/workflows/s3_image_upload.yaml) <br>
This Workflow builds a Docker image as a ZIP archive and then uploads it to an S3 bucket.

> Currently only buckets with _default SSE encryption_ are supported. Support for buckets encrypted with a user-managed KMS key may be added in the future.

</div>

### Semantic Release

<div style="padding-left:20px;">

[release.yaml](/.github/workflows/release.yaml) <br>
This Workflow uses Semantic Release to publish a GitHub release.

</div>

---

## 📖 Relevant GitHub Documentation

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
