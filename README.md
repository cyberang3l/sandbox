####################################
# Sysdata-collector Usage Examples #
####################################

[metadata](#metadata)


### Metadata
asdasdasd
asd
as
da
sd
as
d


### Print a list of the available command line options ###
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

Start collecting data and print the output in STDOUT
When -j is used, there is no output redirected in a file.
```
$ ./sysdata-collector.py -j
```

-------

Print a list of the available plugins located in the
'plugins' folder. Keep in mind, that the plugins located
in the 'plugins' folder are not active by default.

```
$ ./sysdata-collector.py -d
```

-------

Print a list of the active plugins located in the
'active-plugins' folder. To activate a plugin which is
available in the 'plugins' folder, generate a symbolic
link in the active-plugins folder (ln -s plugins/)

```
$ ./sysdata-collector.py -e
```
