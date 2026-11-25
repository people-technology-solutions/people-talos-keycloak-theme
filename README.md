<p align="center">
    <i>🚀 <a href="https://keycloakify.dev">Angular + Vite Keycloakify</a> v11 starter 🚀</i>
    <br/>
    <br/>
</p>

This starter is based on Vite and Angular. There is also [a native esbuild Angular starter](https://github.com/keycloakify/keycloakify-starter-angular).

# Releases

Versions and releases come from [release-please](https://github.com/googleapis/release-please-action), run by [release.yml](.github/workflows/release.yml) on every push to `main` (configured in [release-please-config.json](release-please-config.json) and [.release-please-manifest.json](.release-please-manifest.json)).

1. **Use conventional commit messages.** PRs are squash-merged with the PR title as the commit message, and [pr-title.yml](.github/workflows/pr-title.yml) checks that the title is one. release-please reads the commits on `main` since the last release:

   | Commit | Bump |
   | --- | --- |
   | `fix(…): …` | patch |
   | `feat(…): …` | minor |
   | `feat(…)!: …` or a `BREAKING CHANGE:` footer | major |
   | `chore`, `docs`, `ci`, `build`, `style`, `refactor`, `test` | none, on their own |

2. **A release PR appears** ("chore(main): release x.y.z"). It bumps `version` in `package.json` and adds the commits to [CHANGELOG.md](CHANGELOG.md). It stays open and collects every releasable change until you merge it. Never bump the version by hand.
3. **Merge it** to release. The workflow creates the GitHub Release `vX.Y.Z`, builds the theme from the tag, and attaches `keycloakify-aade-theme.jar` (with a `.sha256`).
4. **people-talos-keycloak is notified** with a `keycloak-theme-released` dispatch, so it can open the PR that bumps its pin.

To release something that isn't a `feat` or `fix` on its own, add a `Release-As: x.y.z` footer to its commit message.

The repository is public, so a release's jar downloads without a token:

```bash
curl -fLO https://github.com/people-technology-solutions/people-talos-keycloak-theme/releases/download/v1.0.0/keycloakify-aade-theme.jar
```

Pull requests still build the jar ([verify.yml](.github/workflows/verify.yml)) and attach it to the run as an artifact, for trying a change before it's released.

The release workflow runs with short-lived tokens from the org's CI GitHub App: the org variable `CI_APP_CLIENT_ID` (the app's Client ID) and the org secret `CI_APP_PRIVATE_KEY`. A PR opened with the workflow's own `GITHUB_TOKEN` wouldn't trigger the release PR's checks.

# Quick start

```bash
git clone https://github.com/keycloakify/keycloakify-starter-angular-vite
cd keycloakify-starter-angular-vite
yarn install # Or use an other package manager, just be sure to delete the yarn.lock if you use another package manager.
```

# Testing the theme locally

[Documentation](https://docs.keycloakify.dev/testing-your-theme)

# How to customize the theme

[Documentation](https://docs.keycloakify.dev/customization-strategies)

# Building the theme

You need to have [Maven](https://maven.apache.org/) installed to build the theme (Maven >= 3.1.1, Java >= 7).  
The `mvn` command must be in the $PATH.

- On macOS: `brew install maven`
- On Debian/Ubuntu: `sudo apt-get install maven`
- On Windows: `choco install openjdk` and `choco install maven` (Or download from [here](https://maven.apache.org/download.cgi))

```bash
npm run build-keycloak-theme
```

Note that by default Keycloakify generates multiple .jar files for different versions of Keycloak.  
You can customize this behavior, see documentation [here](https://docs.keycloakify.dev/features/compiler-options/keycloakversiontargets).

# Initializing the account theme

```bash
npx keycloakify initialize-account-theme
```

# Initializing the email theme

```bash
npx keycloakify initialize-email-theme
```
