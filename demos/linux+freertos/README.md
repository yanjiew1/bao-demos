# Linux+FreeRTOS Demo

This demo features a dual guest configuration, Linux and FreeRTOS, connected 
through inter-VM communication object which is nothing more than a shared 
memory region and doorbell mechanism in the form of hardware interrupts.

One of the platform's cores is assigned to FreeRTOS while all others are 
used by Linux. The platform's first available UART is also assigned to FreeRTOS.
If anyother UART device is available it is assigned to Linux. If not through a 
UART, the Linux guest is also accessible via ssh at the static address
**192.168.42.15**.

You can send messages to FreeRTOS by writing to `/dev/baoipc0`. For example:

```
echo "Hello, Bao!" > /dev/baoipc0
```

The FreeRTOS guest will also send a message to Linux each time it receives a 
character in its UART. However, the Linux inter-VM is not configured for Linux
to asynchronously react to it and output this message. You can checkout the last
FreeRTOS message by reading `/dev/baoipc0`:

```
cat /dev/baoipc0
```

Follow the instructions to build [FreeRTOS](../../guests/freertos/README.md) 
and [Linux](../../guests/linux/README.md).