Testflinger job examples
========================================

Here are some examples of Testflinger jobs that can be modified and reused to
quickly get up and running. Most of the modification you'll want to do is in
the `test_cmds` element.

.. _example-dragonboard:

Dragonboard 410c
-----------------------------
Dragonboard can be provisioned by either specifying the URL to an image, or by
specifying the channel you wish to use. If you specify the channel, it will
build a custom image (not official) with the snaps from the specified channel.

URL Method:

.. code-block:: yaml

    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/16/stable/current/ubuntu-core-16-dragonboard.img.xz

Channel Method:

.. code-block:: yaml

    provision_data:
      channel: edge

Full example:

.. code-block:: yaml

    job_queue: dragonboard
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/16/stable/current/ubuntu-core-16-dragonboard.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-cm3:

RPI Compute Module 3 (CM3)
----------------------------

Full example:

.. code-block:: yaml

    job_queue: cm3
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/16/stable/current/ubuntu-core-16-cm3.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-cm3p:

RPI Compute Module 3+ (CM3+)
----------------------------

Full example:

.. code-block:: yaml

    job_queue: cm3p
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/16/stable/current/ubuntu-core-16-cm3.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-rpi3b:

RPI 3B
----------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi3
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

For the full provisioning version of RPI 3B, see :ref:`example-rpi3provision`.

.. _example-rpi3bplus:

RPI 3B+
----------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi3bp-core18
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

For the full provisioning version of RPI 3B+, see :ref:`example-rpi3provision`.

.. _example-rpi3aplus:

RPI 3A+
----------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi3ap-core18
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

For the full provisioning version of RPI 3A+, see :ref:`example-rpi3provision`.

.. _example-rpi3provision:

RPI 3B, 3B+, 3A+  with full provisioning
----------------------------------------

For the RPI 3B, 3B+, and 3A+ will full provisioning, they all work basically
the same as the ones above, except you need to use a new queue name and specify
an image to use.

.. warning::
    Avoid using a core18 image with rpi3A+ for full provisioning, or a core16 image with rpi3A+ for now. Due to known bugs on each, they may not boot properly.

Here's a full example for RPI3B, using a core18 image:

.. code-block:: yaml

    job_queue: rpi3b
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/18/stable/current/ubuntu-core-18-armhf+raspi3.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

Make sure to change the queue to: rpi3b, rpi3bp, or rpi3ap for the full
provisioning version of RPI3B, B+, and A+ respectively.

Other images you may want to consider using:

.. csv-table::
    :header: "Image type", "URL"

    "Core 16 ", "``http://cdimage.ubuntu.com/ubuntu-core/16/stable/ubuntu-core-16-pi3.img.xz``"
    "Core 18 ", "``http://cdimage.ubuntu.com/ubuntu-core/18/stable/current/ubuntu-core-18-armhf+raspi3.img.xz`` "
    "Bionic armhf ", "``http://cdimage.ubuntu.com/ubuntu-server/bionic/daily-preinstalled/current/bionic-preinstalled-server-armhf+raspi3.img.xz`` "
    "Bionic arm64 ", "``http://cdimage.ubuntu.com/ubuntu-server/bionic/daily-preinstalled/current/bionic-preinstalled-server-arm64+raspi3.img.xz`` "
    "Disco armhf ", "``http://cdimage.ubuntu.com/ubuntu-server/daily-preinstalled/current/disco-preinstalled-server-armhf+raspi3.img.xz`` "
    "Disco arm64 ", "``http://cdimage.ubuntu.com/ubuntu-server/daily-preinstalled/current/disco-preinstalled-server-arm64+raspi3.img.xz`` "

.. _example-rpi2:

RPI 2
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi2
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/18/stable/current/ubuntu-core-18-armhf+raspi2.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-rpi4b1g:

RPI 4 1GB
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi4b1g
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/18/stable/current/ubuntu-core-18-arm64+raspi4.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-rpi4b2g:

RPI 4 2GB
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi4b2g
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/18/stable/current/ubuntu-core-18-arm64+raspi4.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-rpi4b4g:

RPI 4 4GB
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi4b4g
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-core/18/stable/current/ubuntu-core-18-arm64+raspi4.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-rpi4b8g:

RPI 4 8GB
----------------------------------

.. warning::
   18.04/UC18 is not yet supported on this device, but UC20 and Focal server are supported

Full example:

.. code-block:: yaml

    job_queue: rpi4b8g
    provision_data:
      url: http://cdimage.ubuntu.com/releases/20.04/release/ubuntu-20.04-preinstalled-server-arm64+raspi.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-rpi400:

RPI 400
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: rpi400
    provision_data:
      url: http://cdimage.ubuntu.com/releases/groovy/release/ubuntu-20.10-preinstalled-desktop-arm64+raspi.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-cm4lite:

RPi CM4
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: rpicm4l
    provision_data:
      url: http://cdimage.ubuntu.com/releases/groovy/release/ubuntu-20.10-preinstalled-server-arm64+raspi.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-stlouis:

Dell St. Louis
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: stlouis
    provision_data:
      url: http://10.102.196.9/plano/stlouis-current.img.xz
    test_data:
      test_username: admin
      test_password: admin
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-caracalla-media:

Dell Caracalla (Media SKU)
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: caracalla-media
    provision_data:
      url: http://10.102.196.9/plano/caracalla-current.img.xz
    test_data:
      test_username: admin
      test_password: admin
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-caracalla-transport:

Dell Caracalla (Transport SKU)
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: caracalla-transport
    provision_data:
      url: http://10.102.196.9/plano/caracalla-current.img.xz
    test_data:
      test_username: admin
      test_password: admin
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-caracalla-gpa:

Dell Caracalla (GPA SKU)
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: caracalla-gpa
    provision_data:
      url: http://10.102.196.9/plano/caracalla-current.img.xz
    test_data:
      test_username: admin
      test_password: admin
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-rigado:

Rigado
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: tillamook
    test_data:
      test_username: admin
      test_password: ubuntu
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-dawson:

Dawson
----------------------------------

Dawson is an Intel NUC device. They can be provisioned via MAAS. You can
provision these identically to the way the other MAAS devices are provisioned, 
but you should use the image ``dawson-uc18-m7-20190122-10``.  The queues for 
these devices are:

* dawson-i
* dawson-j

Full example:

.. code-block:: yaml

    job_queue: dawson-i
    provision_data:
      distro: dawson-uc18-m7-20190122-10
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP snap list
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-unleashed:

Unleashed
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: unleashed
    provision_data:
      url: http://cdimage.ubuntu.com/ubuntu-server/daily-preinstalled/current/impish-preinstalled-server-riscv64+unleashed.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

.. _example-unmatched:

Unmatched
----------------------------------

Full example:

.. code-block:: yaml

    job_queue: unmatched
    provision_data:
     url: http://cdimage.ubuntu.com/ubuntu-server/daily-preinstalled/current/impish-preinstalled-server-riscv64+unmatched.img.xz
    test_data:
      test_cmds: |
        ssh ubuntu@$DEVICE_IP cat /proc/cpuinfo

