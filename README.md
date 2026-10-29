# synnical-repo

This is the official package repository for [Synnical](https://github.com/voltiksrc/synnical), a source-based system manager written in C++23.

The repository contains package recipes, source URLs, checksums, dependencies, and other metadata used by Synnical to download, build, and install software.

Synnical uses TOML for its package recipes and libsolv for dependency resolution.

## Repository Structure

```text
synnical-repo/
├── index.toml
├── packages.solv
└── packages/
    ├── zlib/
    │   └── package.toml
    ├── libpng/
    │   └── package.toml
    └── ...
```

- `index.toml` lists the available packages and their recipe locations.
- `packages.solv` contains repository metadata used by the dependency solver.
- `packages/` contains the individual TOML recipes.

## Package Recipes

Every package has its own directory containing a `package.toml` file.

A basic recipe looks like this:

```toml
[package]
name = "zlib"
version = "1.3.2"
architecture = "x86_64"

[source]
url = "https://example.org/source.tar.gz"
sha256 = "..."

[build]
system = "make"

[deps]
requires = []
build_requires = []
```

The recipe tells Synnical where to download the source, how to verify it, which build system to use, and what dependencies are needed.

The example above is simplified. Actual recipes must use valid source URLs and SHA-256 checksums.

## Submitting Packages

If you would like a package added to the repository, you can open an issue or submit a pull request.

There are a few requirements:

1. Packages must not depend on a specific init system.
2. Recipes must follow the expected TOML format.
3. Packages must be tested using Synnical before submission.
4. Source URLs and checksums must be valid.
5. Dependencies should be listed correctly, including build dependencies.

Not every package will work immediately, especially while Synnical's build system support is still being improved and worked on.

If a recipe needs special handling, explain it in your pull request please.

## Repository Updates

The package index and solver metadata are maintained separately.

When recipes or dependencies change, `packages.solv` needs to be regenerated so Synnical can resolve the updated package information.

For development, the metadata generator is available through the main Synnical repository:

```bash
cmake --build build --target generate-solv
```

This currently expects the Synnical repository and `synnical-repo` to be located in neighboring directories.

## Goal

The current goal is to reach 100 packages, But the REAL goal is packages that build reliably rather than adding as many as possible.

The repository is still small and under active development. More packages and improvements will be added as Synnical progresses.

## Contributing

Contributions are welcome, whether it's a new package, a corrected dependency, an updated checksum, or a fix to an existing recipe.

For changes to the package manager itself, visit the [Synnical repository](https://github.com/voltiksrc/synnical).

## License

This repository is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.
