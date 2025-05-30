Eclipse Mosquitto
=================

Mosquitto is an open source implementation of a server for version 5.0, 3.1.1,
and 3.1 of the MQTT protocol. It also includes a C and C++ client library, and
the `mosquitto_pub` and `mosquitto_sub` utilities for publishing and
subscribing.

## Links

See the following links for more information on MQTT:

- Community page: <http://mqtt.org/>
- MQTT v3.1.1 standard: <https://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.html>
- MQTT v5.0 standard: <https://docs.oasis-open.org/mqtt/mqtt/v5.0/mqtt-v5.0.html>

Mosquitto project information is available at the following locations:

- Main homepage: <https://mosquitto.org/>
- Find existing bugs or submit a new bug: <https://github.com/eclipse/mosquitto/issues>
- Source code repository: <https://github.com/eclipse/mosquitto>

There is also a public test server available at <https://test.mosquitto.org/>

## Installing

See <https://mosquitto.org/download/> for details on installing binaries for
various platforms.

## Quick start

If you have installed a binary package the broker should have been started
automatically. If not, it can be started with a very basic configuration:

    mosquitto

Then use `mosquitto_sub` to subscribe to a topic:

    mosquitto_sub -t 'test/topic' -v

And to publish a message:

    mosquitto_pub -t 'test/topic' -m 'hello world'

Note that starting the broker like this allows anonymous/unauthenticated access
but only from the local computer, so it's only really useful for initial testing.

If you want to have clients from another computer connect, you will need to
provide a configuration file. If you have installed from a binary package, you
will probably already have a configuration file at somewhere like
`/etc/mosquitto/mosquitto.conf`. If you've compiled from source, you can write
your config file then run as `mosquitto -c /path/to/mosquitto.conf`.

To start your config file you define a listener and you will need to think
about what authentication you require. It is not advised to run your broker
with anonymous access when it is publically available.

For details on how to do this, look at the
[authentication methods](https://mosquitto.org/documentation/authentication-methods/)
available and the [dynamic security plugin](https://mosquitto.org/documentation/dynamic-security/).

## Documentation

Documentation for the broker, clients and client library API can be found in
the man pages, which are available online at <https://mosquitto.org/man/>. There
are also pages with an introduction to the features of MQTT, the
`mosquitto_passwd` utility for dealing with username/passwords, and a
description of the configuration file options available for the broker.

Detailed client library API documentation can be found at <https://mosquitto.org/api/>

## Building from source

To build from source the recommended route for end users is to download the
archive from <https://mosquitto.org/download/>.

On Windows and Mac, use `cmake` to build. On other platforms, just run `make`
to build. For Windows, see also `README-windows.md`.

If you are building from the git repository then the documentation will not
already be built. Use `make binary` to skip building the man pages, or install
`docbook-xsl` on Debian/Ubuntu systems.

### Build Dependencies

* c-ares (libc-ares-dev on Debian based systems) - only when compiled with `make WITH_SRV=yes`
* cJSON - for client JSON output support. Disable with `make WITH_CJSON=no` Auto detected with CMake.
* libwebsockets (libwebsockets-dev) - enable with `make WITH_WEBSOCKETS=yes`
* openssl (libssl-dev on Debian based systems) - disable with `make WITH_TLS=no`
* pthreads - for client library thread support. This is required to support the
  `mosquitto_loop_start()` and `mosquitto_loop_stop()` functions. If compiled
  without pthread support, the library isn't guaranteed to be thread safe.
* uthash / utlist - bundled versions of these headers are provided, disable their use with `make WITH_BUNDLED_DEPS=no`
* xsltproc (xsltproc and docbook-xsl on Debian based systems) - only needed when building from git sources - disable with `make WITH_DOCS=no`

Equivalent options for enabling/disabling features are available when using the CMake build.


## Credits

Mosquitto was written by Roger Light <roger@atchoo.org>
