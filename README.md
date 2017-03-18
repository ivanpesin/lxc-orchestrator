# puppet-demo-lxc-env

Scripts to create and manage demo LXC environment with puppet servers and clients

## Description

* `mk-puppet-lxc.bsh`: creates `LXC` container with puppet CE agent
* `mk-pe-lxc.bsh`: creates `LXC` container with puppet PE agent
* `swarm.bsh`: manages client containers (start/stop/create/destroy)
* `lxc-orchestrator.bsh`: randomly brings clients up and down

## Orchestrator rules

- each day randomly select `P` protected instances and keep
  them running for the whole day
- from remaining `(N-P)` instances randomly select `S` instances,
  start them, let them run for `T` minutes, and then shut them down.
- repeat cycle until day ends or all instances are cycled
- selection should randomly pick only instances that have not run
  today
- if all instances have been cycled and day has not ended yet
  keep last set of instances running till the day end
- if the are more instances that can be cycled with a day
  proceed with cycling till the day end and ignore instances that
  have not been started this day.
