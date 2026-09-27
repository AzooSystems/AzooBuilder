# AzooBuilder

Builder workflows for other repositories

Workflow documentation

<!--
container run --rm -v "$(pwd):/work" -w "/work" \
ghcr.io/tmknom/actdocs inject --sort --file README.md .github/workflows/build-and-release-ps-module.yml
-->

<!-- actdocs start -->

## Inputs

| Name | Description | Type | Default | Required |
| :--- | :---------- | :--- | :------ | :------: |
| moduleName | PowerShell module name | `string` | n/a | yes |
| modulePath | Path to the module source directory | `string` | n/a | yes |
| publishToGitHubContainerRegistry | Publish the module package as an OCI artifact to GitHub Container Registry | `boolean` | `false` | yes |
| publishToGitHubPackagesNuGetFeed | Publish the module to the caller-configured GitHub Packages NuGet feed | `boolean` | `false` | yes |
| publishToGitHubRelease | Create or update the GitHub Release for v{version} and upload the module package | `boolean` | `false` | yes |
| publishToPowerShellGallery | Publish the package to PowerShell Gallery | `boolean` | `false` | yes |
| version | Semantic version without a leading v. PowerGallaery adds some limitations for version scheme. | `string` | n/a | yes |
| generateAttestation | Override attestation generation with true or false; auto generates stable attestations only | `string` | `auto` | no |
| gitHubContainerRegistryOrganizationName | GHCR organization name; defaults to the repository owner | `string` | n/a | no |
| gitHubContainerRegistryPackageName | GHCR package name; defaults to the PowerShell module name | `string` | n/a | no |
| gitHubPackagesNuGetFeedOrganizationName | Organization name used as the credential username for the GitHub Packages NuGet feed | `string` | n/a | no |
| gitHubPackagesNuGetFeedRepositoryName | Local PSResource repository name assigned to the caller's GitHub Packages NuGet feed | `string` | n/a | no |
| gitHubPackagesNuGetFeedUri | NuGet endpoint URI of the caller's GitHub Packages feed | `string` | n/a | no |
| psGalleryRepositoryName | Registered PSResource repository name for PowerShell Gallery | `string` | `PSGallery` | no |

## Secrets

| Name | Description | Required |
| :--- | :---------- | :------: |
| galleryApiKey | API key used to publish to PowerShell Gallery | no |
| gitHubContainerRegistryToken | Token with packages write permission used to publish to GHCR | no |
| gitHubPackagesNuGetFeedToken | Token used to publish to GitHub Packages(nuget feed) | no |
| gitHubReleaseToken | Token used to create or update the GitHub Release | no |

## Outputs

N/A

## Permissions

N/A

<!-- actdocs end -->

## PowerShell

### Download a package from GHCR with ORAS

The GHCR package must have **Public** visibility for downloads without authentication.
A public source repository does not automatically make its packages public.

Install ORAS on macOS:

```shell
brew install oras
```

Download the `.nupkg` without running `oras login`:

```shell
oras pull ghcr.io/organization/package-name:1.2.3 --output ./artifacts
```

Replace `organization`, `package-name`, and `1.2.3` with the published GHCR
organization, lower-case package name, and version. ORAS writes the original
`.nupkg` file into `./artifacts`.
