# AzooBuilder

Builder workflows for other repositories

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
