Supported device types
=======================

Different devices need to be provisioned in slightly different ways, but this is generally transparent to the user. For most devices, all you need to specify is the URL for the image you want to test. If you are interested in more information about supported provisioning methods, refer to :doc:`provisioning-methods`.

For the examples of Testflinger jobs that can be modified and reused to
quickly get up and running on each of the devices, see :doc:`job-examples`

Ubuntu Core devices
---------------------

.. csv-table::
    :header: "Device", "Full Provisioning", "Queue(s)"

    ":ref:`example-dragonboard`", "Yes", "dragonboard"
    ":ref:`example-cm3`", "Yes", "cm3"
    ":ref:`example-cm3p`", "Yes", "cm3p"
    ":ref:`RPI3B Full Provisioning <example-rpi3b>`", "Yes", "rpi3b"
    ":ref:`RPI3B+ Full Provisioning <example-rpi3bplus>`", "Yes", "rpi3bp"
    ":ref:`RPI3A+ Full Provisioning <example-rpi3aplus>`", "Yes", "rpi3ap"
    ":ref:`example-rpi2`", "Yes", "rpi2"
    ":ref:`example-rpi4b1g`", "Yes", "rpi4b1g"
    ":ref:`example-rpi4b2g`", "Yes", "rpi4b2g"
    ":ref:`example-rpi4b4g`", "Yes", "rpi4b4g"
    ":ref:`example-rpi4b8g`", "Yes", "rpi4b8g"
    ":ref:`example-rpi400`", "Yes", "rpi400"
    ":ref:`example-cm4lite`", "Yes", "rpicm4l"
    ":ref:`example-stlouis`", "Yes", "stlouis"
    ":ref:`example-caracalla-media`", "Yes", "caracalla-media"
    ":ref:`example-caracalla-transport`", "Yes", "caracalla-transport"
    ":ref:`example-caracalla-gpa`", "No", "caracalla-gpa"
    ":ref:`example-rigado`", "No", "tillamook"
    ":ref:`Dawson Canyon (Intel NUC) <example-dawson>`", "Yes", "dawson-i"
    ":ref:`June Canyon (Intel NUC) <example-dawson>`", "Yes", "dawson-j"
    ":ref:`HiFive Unleashed (RISC-V) <example-unleashed>`", "Yes", "unleashed"
    ":ref:`HiFive Unmatched (RISC-V) <example-unmatched>`", "Yes", "unmatched"

MAAS devices
----------------

We currently have some x86 systems deployed in MAAS for graphics testing. These
can be used as generic x86 test systems or referenced by the GPU type to select
a specific system with that graphics type.

MAAS images imported from simplestreams can be specified for provisioning such
as xenial, bionic, cosmic, etc. Additionally, we have a number of desktop
images that have been converted with curtinator that can be installed:

* desktop-14-04-curtinator
* desktop-16-04-curtinator
* desktop-17-04-curtinator
* desktop-17-10-curtinator
* desktop-18-04-curtinator
* desktop-18-10-curtinator

Core images can work under MAAS also:

* ubuntu-core-16
* ubuntu-core-18

For provisioning these systems, you can specify either the distro name for the
MAAS image, or one of the above for the desktop/curtinator image.

.. csv-table::
    :header: "System ID", "Device type", "System Details", "Queues"

    "`201507-18601 <https://certification.canonical.com/hardware/201507-18601/>`_", "Dell Inspiron 5759 ", "core i5, 16GB ", "maas-x86-node, amd-gfx "
    "`201501-16351 <https://certification.canonical.com/hardware/201501-16351/>`_", "Dell Inspiron 5758 ", "core i5, 16GB ", "maas-x86-node, nvidia-gfx "
    "`201506-18347 <https://certification.canonical.com/hardware/201506-18347/>`_", "Dell Inspiron 3252 ", "celeron, 2GB ", "maas-x86-node, intel-gfx "
    "`201302-12728 <https://certification.canonical.com/hardware/201302-12728/>`_", "Lenovo ThinkCentre Edge 62z ", "i3-2130, 4GB ", "maas-x86-node, intel-gfx, 201302-12728 "
    "`201903-26932 <https://certification.canonical.com/hardware/201903-26932/>`_", "Dell Precision 5540 ", "i9, 16GB ", "maas-x86-node, 201903-26932, nvidia-gfx "


Here's an example job that would run on any of them. You can replace the queue
with one of the specific queues mentioned above to request a specific node:

.. code-block:: yaml

    job_queue: maas-x86-node
    provision_data:
      distro: xenial
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo
        ssh ubuntu@$DEVICE_IP ifconfig


In the provision_data, you can also specify the kernel to use, if you need to
use something other than the default. The string specified here is just passed
on to MaaS CLI with the hwe_kernel= parameter, in the same way the distro is
specified. Example:

.. code-block:: yaml

    provision_data:
      distro: bionic
      kernel: hwe-18.04
