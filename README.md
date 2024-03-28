# repowand 🪄

`repowand` is a command-line utility for querying Repology's API, and is useful
for users and developers who:
* Need to compare package versions and metadata between software distributions
frequently.
* Require specific software on multiple PCs with different operating
systems/toolchains, often needing to switch between them.
* Want to avoid maintaining a bunch of lists of the same packages for different
repositories.

## Getting Started

Other than Python 3, no dependencies are required to run Repowand.
```
 > ./repowand
```

```
 > python3 repowand
```

Copy or symlink `repowand` to a directory in your `$PATH` to use it anywhere.
```
 > # Assuming ~/.local/bin is in your $PATH, and your current directory is this repo.
 > ln -s $(realpath ./repowand) ~/.local/bin
 > repowand
```
Make sure `repowand` has executable permissions with `chmod +x ./repowand`

## Subcommands

Simply typing `repowand` will just print its help message.
The real magic is in these subcommands:

* `repowand mklist -R repo ~/path/to/template.json`
can produce lists of packages matching names from any given repo(s) from a
template, easily usable in package management/bootstrap scripts.
  * Advanced per-repository control of list generation is possible using regex
  to select both repository names and package names.
  * See `mklist-example.yaml` and
  `mklist-example.json` for example templates.
    * YAML configuration is only supported if you have PyYAML installed.

* `repowand compare packagename list,of,fields` 
can output package metadata from Repology in script-friendly columns. The 
supported fields are:
  * **name**: Equivalent to **binname** if present, or **srcname** if not.
  * **srcname, binname**: Package name(s) as used in repository - source package
  name and/or binary package name, whichever is applicable.
  * **repo**: Repository name, including distribution version if applicable.
  * **subrepo**: Subrepository name, if applicable. (for example, main or
  contrib or non-free from Debian)
  * **visiblename**: Package name as shown to the user by Repology.
  * **version**: Package version. (sanitized, as shown by Repology)
  * **origversion**: Package version as in repository.
  * **status**: Package status. (newest, devel, unique, outdated, legacy,
  rolling, noscheme, incorrect, untrusted, ignored)
  * **summary**: One-line description of the package.
  * **categories**: List of categories for the package.
  * **licenses**: List of licenses for the package.
  * **maintainers**: List of package maintainers.

## Flags

These all apply to both subcommands.

* `-R REPOS, --repos REPOS`: Specify repository(s) to search for packages in. 
Required for `mklist`.
* `-c, --ignore-cached`: Re-download package data, even if it's cached.
* `-q, --count-api-queries`: Show the total number of API queries when the 
program exits.

### License

Copyright (c) 2024 Amber Connelly

This software is licensed under the MIT License. See LICENSE.txt for details.
