# Meerschaum Compose Project Template

This template is for quickly building Dockerized [Meerschaum Compose](https://meerschaum.io/reference/compose/) projects. For a more detailed example, refer to the [Tech Slam 'N Eggs example repository](https://github.com/bmeares/techslamneggs).

> Docker is not required but `docker/Dockerfile` is provided for convenience.

### Plugins

Meerschaum's [plugin system](https://meerschaum.io/reference/plugins/) allows you to do the following:
- **Quickly ingest data**  
  [`fetch()`](https://meerschaum.io/reference/plugins/writing-plugins/#the-fetch-function) or [`sync()`](https://meerschaum.io/reference/plugins/writing-plugins/#the-sync-function)
- **Add custom connectors**  
  [`@make_connector`](https://meerschaum.io/reference/connectors/#-environment-connectors)
- **Define custom actions**  
  [`@make_action`](https://meerschaum.io/reference/plugins/writing-plugins/#the-make_action-decorator)
- **Add command-line arguments**  
  [`add_plugin_argument()`](https://meerschaum.io/reference/plugins/writing-plugins/#custom-command-line-options)
- **Extend the web API**  
  [`@api_plugin`](https://meerschaum.io/reference/plugins/writing-plugins/#the-api_plugin-decorator)

Consult the [plugins documentation](https://meerschaum.io/reference/plugins/writing-plugins/) for how to write your own plugins. The plugin `example` has been added as reference for `plugin:example` and `example:{label}`.

## Getting Started

Build and start the container:

```bash
docker compose up --build -d
```

Jump into a shell:

```bash
docker compose exec -it mrsm-compose bash
```

Once inside the container, you may now make changes and begin your development process. Here are some useful commands to get started:

```bash
mrsm compose explain
```

This will parse your compose file and print your current environment and state of the pipes.

```bash
mrsm compose run
```

The default command in `docker/bootstrap.sh` is `mrsm compose run` because it does the following:
- Register and update the parameters for your pipes.
- Sync them one-by-one.

Flags you pass to `compose run` are passed to `sync pipes`, including custom arguments added via []`add_plugin_argument()`](https://meerschaum.io/reference/plugins/writing-plugins/#custom-command-line-options).

## Publishing Your Plugins

If you choose to publish your plugins to the public repository, make an account at https://api.mrsm.io and run the `register plugin command`, e.g. (assuming `my-awesome-plugin.py` exists):

```bash
mrsm compose login api:mrsm
mrsm compose register plugin my-awesome-plugin
```

You may also publish your plugins to your private repository with `--repository` or `-r`:

```bash
### Define api:private through the wizard.
### On your repository's host, start the repository with `mrsm start api`.
mrsm compose bootstrap connector
mrsm compose register plugin my-awesome-plugin -r api:private
```
