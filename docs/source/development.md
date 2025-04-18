# Development

```{include} ../../CONTRIBUTING.md
```

## Video tutorial

A short video tutorial on how to build a custom firmware version:

<iframe width="720" height="405" src="https://rutube.ru/play/embed/1ff6fc7246260b3d404acebd0435d785?p=faQjyf7QWhT3bff2GDrReQ" frameBorder="0" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>

## Compiling the source code

1. Install [Arduino CLI](https://arduino.github.io/arduino-cli/1.2/installation/).
2. Go to the repository root folder
3. Compile and flash the firmware

``` shell
arduino-cli compile --clean -e -p COM_PORT -u ats-mini
```

## Adding a changelog entry

1. Install `uv` <https://docs.astral.sh/uv/getting-started/installation/>
2. Run `uv sync`
3. Create an entry:
   ```
   uv run towncrier create --edit ID.CATEGORY.md
   ```
   `ID` is an issue or a PR number, or `+STRING` if there is no issue/PR. `CATEGORY` is one of `added`, `changed`, `fixed`, etc. see the `tool.towncrier.type` sections in the `pyproject.toml` for the full list.

## Improving the documentation

1. Install `uv` <https://docs.astral.sh/uv/getting-started/installation/>
2. Run `uv sync`
3. Run a local webserver `uv run sphinx-autobuild docs/source docs/build` and open the http://127.0.0.1:8000 in a browser
4. Edit the Markdown files in `docs/source` folder and immediately see your changes reflected in the browser

## Release process

1. Bump the `app_ver` and `app_date` constants in the `ats-mini.ino` file
2. If the new version has a different EEPROM layout, bump the `app_id` as well (it will force the EEPROM reset)
3. Generate the CHANGELOG.md by running `uv run towncrier build --version X.XX`
4. Add and commit the changes with a message like "Release X.XX", then push them to the repository
5. Once the build is complete, download, flash and test it!
6. Tag the release and push the tag `git tag -a vX.XX -m 'Version X.XX' && git push --follow-tags` (the tag should start with `v`!)
