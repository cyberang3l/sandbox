####################################
# Sysdata-collector Usage Examples #
####################################

* [Print a help message](#print-a-help-message)
* [Collect data and print the output in STDOUT](#collect-data-and-print-the-output-in-stdout)
* [List the available plugins](#list-the-available-plugins)
* [List the active plugins](#list-the-active-plugins)





### Print a help message

A list of the available command line options
```
$ ./sysdata-collector.py -h
usage: sysdata-collector.py [-h] [-v] [-a] [-b FILE] [-c CHAR] [-d] [-e]
                            [-f DIR] [-g PLUGIN.py] [-i FLOAT] [-j]
                            [-C conf_file] [-D] [-Q] [-L log_level]
                            [-F log_file]

sysdata-collector version 0.0.1

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -a, --append-file     If the FILE exists, append to the end of the file.
                        Otherwise, create a new one with an extended filename.
  -b FILE, --output-file FILE
                        Filename to save the collected data file
  -c CHAR, --delimiter CHAR
                        CHAR is a single character to be used for field
                        separation in the output FILE
  -d, --list-available-plugins
                        Prints a list of the available plugins and exit
  -e, --list-active-plugins
                        Prints a list of the active plugins located under the
                        chosen active-directory and exit
  -f DIR, --active-dir DIR
                        Define the active-directory to load plugins from for
                        this experiment.
  -g PLUGIN.py, --plugin-test PLUGIN.py
                        Use this option for debugging newly created plugins
  -i FLOAT, --interval-between-samples FLOAT
                        A FLOAT number which is the sleeping time given in
                        seconds between sampling. If the value is 0 or
                        negative, instant sampling will be initiated after
                        each previous one
  -j, --only-print-samples
                        Enabling this flag, will disable saving samples in a
                        file. They will only be printed instead.
  -C conf_file, --conffile conf_file
                        conf_file where the configuration will be read from
                        (Default: will search for file 'sysdata-
                        collector.conf' in the known predefined locations
  -D, --daemon          run in daemon mode

Logging Options:
  List of optional logging options

  -Q, --quiet           Disable logging in the console but still keep logs in
                        a file. This options is forced when run in daemon
                        mode.
  -L log_level, --loglevel log_level
                        log_level might be set to: CRITICAL, ERROR, WARNING,
                        INFO, DEBUG. (Default: INFO)
  -F log_file, --logfile log_file
                        log_file where the logs will be stored. If the file
                        exists, text will be appended, otherwise the file will
                        be created (Default: ./sysdata-collector.log)
```
-------

### Collect data and print the output in STDOUT

Start collecting data and print the output in STDOUT.
When `-j` is used, there is no output redirected in a file.

An example printout of my system with the `CPU` and `NET` plugins activated:
```
$ ./sysdata-collector.py -j
datetime,timestamp,eth0_rx_bytes,eth0_tx_bytes,eth0_rx_packets,eth0_tx_packets,eth0_rx_errs,eth0_tx_errs,eth0_rx_drop,eth0_tx_drop,wlan0_rx_bytes,wlan0_tx_bytes,wlan0_rx_packets,wlan0_tx_packets,wlan0_rx_errs,wlan0_tx_errs,wlan0_rx_drop,wlan0_tx_drop,cpus_avg_user,cpus_avg_nice,cpus_avg_system,cpus_avg_idle,cpus_avg_iowait,cpus_avg_irq,cpus_avg_softirq,cpus_avg_steal,cpus_avg_guest,cpus_avg_guest_nice,cpus_avg_percent,cpu_0_user,cpu_0_nice,cpu_0_system,cpu_0_idle,cpu_0_iowait,cpu_0_irq,cpu_0_softirq,cpu_0_steal,cpu_0_guest,cpu_0_guest_nice,cpu_0_percent,cpu_1_user,cpu_1_nice,cpu_1_system,cpu_1_idle,cpu_1_iowait,cpu_1_irq,cpu_1_softirq,cpu_1_steal,cpu_1_guest,cpu_1_guest_nice,cpu_1_percent,cpu_2_user,cpu_2_nice,cpu_2_system,cpu_2_idle,cpu_2_iowait,cpu_2_irq,cpu_2_softirq,cpu_2_steal,cpu_2_guest,cpu_2_guest_nice,cpu_2_percent,cpu_3_user,cpu_3_nice,cpu_3_system,cpu_3_idle,cpu_3_iowait,cpu_3_irq,cpu_3_softirq,cpu_3_steal,cpu_3_guest,cpu_3_guest_nice,cpu_3_percent,ctxt,btime,processes,procs_running,procs_blocked
2014-04-23_23:15:50,1398287750134953,148694350,3233934013,1246709,2226310,0,0,0,0,0,0,0,0,0,0,0,0,343849,2212,92796,4472905,28768,39141,0,0,0,0,7.91,85024,623,27732,1112266,6934,11735,0,0,0,0,18.18,90917,524,17971,1111823,6897,17252,0,0,0,0,1.03,86517,440,28476,1117942,6087,5113,0,0,0,0,5.1,81389,624,18616,1130872,8849,5039,0,0,0,0,5.21,28844656,1398282476,19703,3,0
```

-------

### List the available plugins

List the available plugins located in the `plugins` folder.
Keep in mind, that the plugins located in the `plugins`
folder are not active by default.

```
$ ./sysdata-collector.py -d
Getting available plugins in the system...
4 plugins available.
#######################################
List of available plugins:
    1: 'Kernel Version Version 1.0' located at '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/plugins/kernel_version.py'
         Module name: 'kernel_version.py'
    2: 'CPU Stats Version 0.2' located at '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/plugins/cpu.py'
         Module name: 'cpu.py'
    3: 'Net Stats Version 0.1' located at '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/plugins/net.py'
         Module name: 'net.py'
    4: 'New plugin template Version 0.0.1' located at '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/plugins/new_plugin_template.py'
         Module name: 'new_plugin_template.py'
```

-------

### List the active plugins

List of the active active plugins located in the `active-plugins` folder.
To activate a plugin which is available in the `plugins` folder,
generate a symbolic link in the active-plugins folder (`ln -s plugins/`)

```
$ ./sysdata-collector.py -e
Getting available plugins in the system...
4 plugins available.
Activating symlinked plugins located in 'active-plugins'
2 plugin(s) activated
#######################################
List of active plugins in directory 'active-plugins'
    1: 'Net Stats Version 0.1' located at '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/plugins/net.py'
         Module name: 'net.py'
         Symlink loading this instance: '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/active-plugins/net.py'
    2: 'CPU Stats Version 0.2' located at '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/plugins/cpu.py'
         Module name: 'cpu.py'
         Symlink loading this instance: '/home/cyber/Dropbox/Various/Scripts/Python/sysdata-collector/active-plugins/cpu.py'
```
