PipeD
=====

A network daemon that runs on the [Node.js][node] platform and
listens for incoming data via one of `UDP, TCP, Unix Socket, File
or STDIN` and sends it out to one (or more) of `UDP, TCP, Unix Socket
or STDOUT`. PipeD can both fanout and failover as needed.

On tests using [c1.medium][c1_medium] PipeD can handle 85k messages/second
over `TCP` or [UDP][udp] with a single output. The bottlenecks are
the `cat` and `nc` process that are taking up the majority of the CPU
for the benchmark.

![overview](https://github.com/jib/piped/raw/master/docs/media/overview.jpg)

Concepts
--------

* *remotes*
  `PipeD` will send your data to one or more remote endpoints. It can
  do a `one to one`, `many to one`, and `many to many` mapping (which
  allows for both fan out and consolidation). It also monitors the
  health of the remotes, failing over to a backup remote as needed.

* *listeners*
  `PipeD` can listen for input in any way that you can do cross process
  communication in your favourite Unix environment. Any input point is
  called a `listener`

Examples
--------

The easiest way to show how `PipeD` works is through some examples:



Debugging
---------

There are additional config variables available for debugging:

* `debug` - log common operations to stderr
* `trace` - log extensive information about all operations to stderr

For more information, check the `etc/config.js.example` file.

Installation and Configuration
------------------------------

 * Install node.js
 * Clone the project
 * Create a config file `from etc/config.js.example` and put it somewhere
 * Start the Daemon:

    node bin/piped.js --config=/path/to/config

 (optional: all config values can be passed on the command line as well)

Tests
-----

`PipeD` comes with a test harness to exercise it's core features. To run
the test suite, run the following command from the repository root:

  $ ./run_tests.sh

Contribute
---------------------

You're interested in contributing to PipeD? *AWESOME*. Here are the basic steps:

fork StatsD from here: http://github.com/jib/piped

1. Clone your fork
2. Hack away
3. If you are adding new functionality, document it in the README
4. If necessary, rebase your commits into logical chunks, without errors
5. Push the branch up to GitHub
6. Send a pull request to the jib/piped project.

We'll do our best to get your changes in!


[krux]: http://www.krux.com
[node]: http://nodejs.org
[udp]: http://en.wikipedia.org/wiki/User_Datagram_Protocol
[c1_medium]: http://aws.amazon.com/ec2/#instance
