Provisioning Methods
===================================

The way provisioning is accomplished can be very different from one type of device to the next. These are the basic provisioning methods currently supported by Testflinger device connectors.

MAAS
-------------------

MAAS devices can be provisioned using the ``maas-cli``.  All the user needs to
specify in the provision data section is ``distro: <name>`` to tell MAAS which
image to use.  In the background, there will need to be a user authenticated
through ``maas-cli`` for the MAAS server where this device is hosted. The device
agent configuration needs to know the ``maas-cli`` user and the system ID in MAAS,
but all this is transparent to the end user.

MuxPi
-------------------

This is a new provisioning method that allows us to reliably and fully reinstall
systems that boot from a Micro SD card.  This includes all Raspberry Pis except
CM3 and Dragonboard.  MuxPi provides SD multiplexing, allowing it to write an
image to the card, then switch control back to the device under test, and turn
on power to the DUT.  This can only be used for devices that boot from SD, but
that encompasses a large number of devices that are tricky to automate
otherwise.  All the user needs to provide is a URL to the image they want to
install and the device connector takes care of the rest.  Even if the image is bad, or fails to boot, recovery is possible.

CM3
-------------------

The Compute Module 3 devices have an EMMC that they can boot from, so images
must be installed to the EMMC before booting. There's a tool for pushing the
image to EMMC from another system via USB.  To facilitate this, the USB cable
must be connected with the right DIP switch settings enabled, and then
disconnected to allow it to boot from the EMMC. We automate this using a
Raspberry PI as a sidecar device to write the image over USB. It is also
equipped with a relay to turn on/off power to the USB cable, simulating 
disconnection so the device can boot from EMMC once the image is written.  This
works very reliably and recovery is possible even if the image is bad or fails
to boot.  All the user needs to provide is the URL for the image to install.

Dragonboard
-------------------

Before MuxPi was available, automated provisioning on Dragonboard was made
possible by booting a static image from the EMMC, writing the test image to the
SD card from there, then rebooting.  Recovery back to booting from the static
image on the EMMC is possible by wiping out the SD card.  This is generally very
reliable, but there are a few pathological cases where this can fail.  Recovery
is simple and rarely needed.  It only requires booting with the SD card
ejected.  These devices will use MuxPi in the future to eliminate the
possibility of failure to provision in this way.  If for any reason a device
can't be recovered to a provisionable state, it is marked offline and the job is
requeued so another device can run it.  The user only needs to provide the URL
for the image they want provisioned.

Netboot
-------------------

A few OEM devices have older images that don't currently work well with MAAS,
but they are capable of network booting.  For these devices, we use a generic
netboot image that has a small tool embedded in it that we use to write the
specified image to the drive on the device, then reboot it.  This works well and
only requires the user to provide the URL, but MAAS is the preferred solution
whenever possible.

Noprovision
-------------------

This is the simplest type of provisioning, it just ensures that the device can
be reached via ssh and reboots it if necessary. Generally, use of noprovision is
restricted to devices for which there's no other current option for automated
installation or recovery.  Care should be taken when working with these devices
to roll back snaps or reset things to a clean state as much as possible.
