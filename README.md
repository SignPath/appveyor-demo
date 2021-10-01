SignPath Demo for AppVeyor deploy hook integration

# Setup

1. On ci.appveyor.com
  * Select Account and Security
    * Make sure the checkboxes for both API v1 and API v2 are checked
  * Select My Profile and API Keys
    * Remember the **Bearer token** for the next step
2. On SignPath.io
  * Create a CI User and remember the **CI user token**
  * Create a Project `My installer`
    * Add an artifact configuration named `v1` for the referenced zip in the `build-output/unsigned` folder
    * Create a signing policy `test-signing` and one `release-signing`
     * Add the CI User as a submitter
    * Link an AppVeyor Trusted Build System
      * Enter the **Bearer token** you just copied from AppVeyor as **API key**
3. On ci.appveyor.com
  * Set up a project linked to this git repository (or a forked version)
  * Set the following environment variables:
    * `SIGNPATH_ORGANIZATION_ID`: the organization ID on SignPath
    * `SIGNPATH_PROJECT_SLUG`: the slug of the project
    * `SIGNPATH_CI_USER_TOKEN`: the **CI user token** you copied from SignPath (_Recommended: Toggle variable encryption on._)

All builds from branches starting with `release` will be signed with the `release-signing` policy, all others with the `test-signing` policy.