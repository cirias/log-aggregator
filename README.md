log-aggregator
==============

Aggregate various project running on different server to one log center.

### Tips

```bash
$ # Check Validation of the config file.
$ rsyslogd -f <config file> -N1
```

### TODO

* analysis situation quantity
* config heartbeat check
* config max error alarm
* make init.d file

### deploy process

It's little different between slave and master server.
These are some step which should be down all the time.

```bash
$ # Update `rsyslog` to 7.*
$ sudo add-apt-repository ppa:adiscon/v7-stable
$ sudo apt-get update
$ sudo apt-get install rsyslog
```

```bash
$ git clone git@github.com:Tradesparq/log-aggregator.git && cd log-aggregator
```

Add option `--merge-logs` to pm2 command.

#### Slave

```bash
$ cp ./rsyslogd.slave.conf /etc/
```

Modify the `/etc/rsyslogd.slave.conf` to fit the special project.

```bash
$ sudo rsyslogd -f/etc/rsyslogd.slave.conf -i/var/run/rsyslogd.slave.pid
```

#### Master

```bash
$ cp ./rsyslogd.master.conf /etc/
```

Modify the `/etc/rsyslogd.master.conf` to fit the special project.

```bash
$ sudo rsyslogd -f/etc/rsyslogd.master.conf -i/var/run/rsyslogd.master.pid
```
