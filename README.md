# 🚧 marathon-dcluster
> A very simple script to create local mesos/marathon cluster for debugging purposes

This python script can be used to deploy a local zookeeper/mesos/marathon cluster in an isolated container for debugging purposes. It's developed using only the core python libraries, so you can use it without any hassle.

# Requirements

- docker & docker-compose
- python 2.6+ (no extra packages needed)

# Usage

Just specify the configuration file to use:

```
./marathon-dcluster path/to/config.file
```

The configuraiton file is a simple `key = value` configuration file that specifies which versions to use, how many instances to launch, which ports to expose and how much resources to allocate.

The minimum required parameters are:

```py
# Which docker image versions to use
mesos = 1.4.0-rc2
marathon = v1.4.7
zookeeper = 3.4
```

## Command-line

The following arguments are frequently used:

* `--rm` : Remove the cluster and remove work directory
* `--reset` : Reset the cluster state by wiping the `/var` contents in the work directory

You can also override each parameter described below. For example:

* `--mesos_master_port 8080`

## Configuration

The full set of available configuration parameters follows, along with their default values:

```py
### Mesos-specific ###

# The mesos version
mesos = None

# The mesos docker image to use
mesos_image = mesosphere/mesos

# How many slaves and masters to start
mesos_masters = 1
mesos_slaves = 1

# Expose mesos 5050 port on the localhost network under the
# specified port. If more than one nodes are started, each
# consecutive node gets the next port allocated.
#
# For example, for `mesos_masters=3` and `mesos_master_port=5050`
# the ports allocated will be `5050`, `5051` and `5052` for each
# individual master.
mesos_master_port = None
mesos_slave_port = None

# You can also override the auto-detected resources and specify
# a custom values for each one.
mesos_resources_cpus = None
mesos_resources_gpus = None
mesos_resources_mem = None
mesos_resources_disk = None

### Marathon-specific ###

# The marathon version
marathon = None

# The marathon docker image to use
marathon_image = mesosphere/marathon

# Additional marathon command-line arguments to pass
marathon_args = None

# Enable JVM debug on marathon and expose the debugger port
# on the localhost, under the specified port
marathon_debug = None

# Expose marathon 8080 port on the localhost network under
# the specified port. If more than one node is started, the same
# rules as for `mesos_master_port` apply.
marathon_port = None

# How many marathon nodes to start
marathon_nodes = 1

### Zookeeper-specific ###

# The marathon version to use
zookeeper = 3.4

# The zookeeper docker image to use
zookeeper_image = zookeeper

# How many zookeeper nodes to start
zookeeper_nodes = 1

# Expose zookeeper 2181 port on the localhost network udner
# the specified port. If more than one node is started, the same
# rules as for `mesos_master_port` apply.
zookeeper_port = None
```
