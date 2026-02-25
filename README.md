# minecraft-server-charts

> [!NOTE]
> This repository is a fork of the excellent work done by [itzg (Geoff Bourne)](https://github.com/itzg) and contributors. Full credit goes to them for the original charts and heavy lifting!
> The original repository can be found at [github.com/itzg/minecraft-server-charts](https://github.com/itzg/minecraft-server-charts).

[![Release Charts](https://github.com/cpfarhood/minecraft-server-charts/actions/workflows/release.yaml/badge.svg)](https://github.com/cpfarhood/minecraft-server-charts/actions/workflows/release.yaml)

## Usage

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Once Helm is set up properly, add the repo as follows:

```console
helm repo add minecraft https://cpfarhood.github.io/minecraft-server-charts
```

You can then run `helm search repo minecraft` to see the charts.

## Charts

* [mc-router](https://github.com/cpfarhood/minecraft-server-charts/tree/master/charts/mc-router)
* [minecraft](https://github.com/cpfarhood/minecraft-server-charts/tree/master/charts/minecraft)
* [minecraft-bedrock](https://github.com/cpfarhood/minecraft-server-charts/tree/master/charts/minecraft-bedrock)
* [minecraft-proxy](https://github.com/cpfarhood/minecraft-server-charts/tree/master/charts/minecraft-proxy)
* [rcon-web-admin](https://github.com/cpfarhood/minecraft-server-charts/tree/master/charts/rcon-web-admin)

```bash
helm install your-release minecraft/minecraft
```

Also see [artifact hub](https://artifacthub.io/packages/search?repo=minecraft-server-charts) for a complete list.
