# minecraft-server-charts

> [!NOTE]
> This repository is a fork of the excellent work done by [itzg (Geoff Bourne)](https://github.com/itzg) and contributors. Full credit goes to them for the original charts and heavy lifting!
> The original repository can be found at [github.com/itzg/minecraft-server-charts](https://github.com/itzg/minecraft-server-charts).

[![](https://git.farh.net/farhoodliquor/minecraft-server-charts/actions/workflows/release.yaml/badge.svg?branch=master)](https://git.farh.net/farhoodliquor/minecraft-server-charts/actions)

## Usage

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Once Helm is set up properly, add the repo as follows:

```console
helm repo add itzg https://git.farh.net/api/packages/farhoodliquor/helm
```

You can then run `helm search repo itzg` to see the charts.

## Charts

* [mc-router](https://git.farh.net/farhoodliquor/minecraft-server-charts/src/branch/master/charts/mc-router)
* [minecraft](https://git.farh.net/farhoodliquor/minecraft-server-charts/src/branch/master/charts/minecraft)
* [minecraft-bedrock](https://git.farh.net/farhoodliquor/minecraft-server-charts/src/branch/master/charts/minecraft-bedrock)
* [minecraft-proxy](https://git.farh.net/farhoodliquor/minecraft-server-charts/src/branch/master/charts/minecraft-proxy)
* [rcon-web-admin](https://git.farh.net/farhoodliquor/minecraft-server-charts/src/branch/master/charts/rcon-web-admin)

```bash
helm install --name your-release itzg/minecraft
```

Also see [artifact hub](https://artifacthub.io/packages/search?repo=minecraft-server-charts) for a complete list.
