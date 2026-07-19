# CreateTrainWorld

A Minecraft modpack built around [Create](https://modrinth.com/mod/create) and its train/rail ecosystem, managed with [packwiz](https://packwiz.infra.link/) and distributed as a Modrinth `.mrpack`.

## Installation

1. Download the latest `createtrainworld-<version>.mrpack` from the [Releases](https://github.com/NotCobaltDragon/CreateTrainWorld/releases) page.
2. Import it into a compatible launcher:
   - **[Prism Launcher](https://prismlauncher.org/)** / **[MultiMC](https://multimc.org/):** Add Instance → Import → select the `.mrpack`.
   - **[Modrinth App](https://modrinth.com/app):** File → Import → select the `.mrpack`.
   - **[ATLauncher](https://atlauncher.com/):** Add Pack → Import → select the `.mrpack`.
3. Launch the instance.

## Repository structure

| Path | Purpose |
|------|---------|
| `pack.toml` | Pack metadata (name, version, Minecraft/loader versions). |
| `index.toml` | packwiz file index and hashes. |
| `mods/` | Per-mod `.pw.toml` metadata files (source of truth, git-tracked). |
| `.github/workflows/` | CI that exports the pack and publishes a release. |

## Development

This pack is managed with [packwiz](https://packwiz.infra.link/). Mods are tracked as individual `.pw.toml` files rather than committing the jars, keeping the repo small and diffable.

### Common commands

```bash
# Add a mod from Modrinth
packwiz modrinth add 

# Update everything to the latest compatible versions
packwiz update --all

# Refresh the index after manual changes
packwiz refresh

# Export a distributable .mrpack locally
packwiz modrinth export
```

## Releasing

Releases are automated via GitHub Actions. Pushing a `v*` tag builds the pack and publishes a release with the `.mrpack` attached:

```bash
# Bump the version in pack.toml first, then:
git tag v1.0.1
git push origin v1.0.1
```

The workflow installs packwiz, runs `packwiz modrinth export -o createtrainworld-<version>.mrpack`, and uploads the result to a new GitHub release. It can also be triggered manually from the **Actions** tab, in which case the version is read from `pack.toml`.
