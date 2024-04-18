Network conditioning
==

Description
--

A macOS script that configures `dummynet` and `pf` for UDP network conditioning during the invocation of a tool. The network is restored when the tool exits. 

Usage
--

```sh
./condition <bandwidth> <packet loss rate> <delay> tool [tool-args]
```

Argument formats:
1. Bandwidth: `n (Kbit/s|Mbit/s)`
2. Packet loss rate: `0.0-1.0` where `0` is no packet loss and `1` is 100% packet loss
3. Delay: `n` in milliseconds

Example
--

```sh
./condition "2000Kbit/s" 0.2 25 file-client -r 10.0.2.20 upload log.txt /home/system/log.txt
```

Notes
--

The filter acts on all UDP packets leaving and arriving at the host for the lifetime of the tool invocation, so other network activity will be affected.

The `restore-net` script can be used to ensure that all dummynet pipes are removed and `pf` restored to default