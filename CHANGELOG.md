# Changelog

All notable changes to this project will be documented in this file.

---

# [1.9.0](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.8.0...v1.9.0) (2024-02-20)


### Features

* add inputs 'node-version-file' and 'dist-dirname' ([d269712](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/d269712121dc68e524a3dfa69cce2f42c7ebdb7a))

# [1.8.0](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.7.2...v1.8.0) (2024-02-15)


### Bug Fixes

* correct vscode dir gitignore pattern ([c2277c7](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/c2277c7c4e33c33df86ef81e6d45407b4cf46436))


### Features

* bump actions/checkout to v4 ([ff096b1](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/ff096b176447862dbfe2b121554822523f6375b3))
* bump SemRel action to v4 ([104acd8](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/104acd88c932157c42ed046fbebefa738520ab5f))
* bump setup-node to v4 ([76cc975](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/76cc975f871d383c53b846c2f4d185bb8d370041))
* rm explicit default SemRel version to use action default ([a8fce5d](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/a8fce5db2685c65488216a244e02d9d57d095ee0))
* rm node-v logic w node-version-file input ([8f2f4ef](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/8f2f4ef216fc102d5c58134644b205d48a3c8a0f))

## [1.7.2](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.7.1...v1.7.2) (2023-10-09)

## [1.7.1](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.7.0...v1.7.1) (2023-07-18)


### Bug Fixes

* add braces around 'cancelled' status check ([42073c6](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/42073c6955c04422aa138fd6a263947abc6dd56d))

# [1.7.0](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.6.0...v1.7.0) (2023-07-18)


### Bug Fixes

* add include=dev to 'npm ci' for build process ([479d656](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/479d656ef3f75442291d563aabdd447015397dc9))


### Features

* ensure job fails if tests fail, replace 'did-tests-succeed' w outcome ([2ed9454](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/2ed945481f863e88c3aac02ad6a130e5f5cc9c01))
* **release:** rm 'release-self' workflow, configure 'release' to run on push ([8c5ce63](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/8c5ce638964697ca0fd26d48e40521451a1f8306))

# [1.6.0](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.5.0...v1.6.0) (2023-07-09)


### Features

* add input 'dockerfile-path' to ecr_image_push ([a0daaf9](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/a0daaf9e974be382dbb33474bae5a8387185ddaf))

# [1.5.0](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.4.4...v1.5.0) (2023-07-09)


### Bug Fixes

* wrap inputs-expr in quotes for bash test ([e370c05](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/e370c0546e6b9816ac1f6bf0fbdc0a7df0f441ef))
* wrap inputs-expr in quotes for bash test ([c809ce6](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/c809ce68bf891e06fccc23226ec5a553d1f146ae))


### Features

* update configure-aws-creds action to v2 ([039e595](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/039e595a6e71de417266e458a4eea1381c8ee593))
* update configure-aws-creds action to v2 ([7acdaf6](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/7acdaf66dca31de23cca3e41813a1ac0368eab15))

## [1.4.4](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.4.3...v1.4.4) (2023-07-08)


### Bug Fixes

* add quotes around inputs.node-version interp for proper sh parsing ([fb6a5ce](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/fb6a5ce76966358d87ad02d12ec6f03c989c239c))

## [1.4.3](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.4.2...v1.4.3) (2023-07-08)


### Bug Fixes

* add '/*' suffix to lts (setup-node uses nvm syntax) ([1337129](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/1337129d94f5d5a61360dea1d7524c1974cbd695))

## [1.4.2](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.4.1...v1.4.2) (2023-07-08)


### Bug Fixes

* rm erroneous leading dot in package-json jq read cmd ([0a091f9](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/0a091f9387a4756f6d87f1cbb7714be4dbbbdc68))

## [1.4.1](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.4.0...v1.4.1) (2023-07-08)

# [1.4.0](https://github.com/Nerdware-LLC/reusable-action-workflows/compare/v1.3.0...v1.4.0) (2023-07-08)


### Bug Fixes

* swap GITHUB_TOKEN for secrets.GITHUB_TOKEN ([c663ed3](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/c663ed35af508ec47a3d3c09378f494d84ab270b))


### Features

* add SemanticRelease config and _release_self workflow ([3070ec2](https://github.com/Nerdware-LLC/reusable-action-workflows/commit/3070ec2ac8f878e4a3e22eec02a0b180ec0287c7))
