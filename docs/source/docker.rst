Docker
======

.. _docker:


Part 1: Overview
----------------

A *container* is a sandboxed process on your machine that is isolated from all other processes on the host machine. To summarize, a container:
* Is a runnable instance of an image. You can create, start, stop, move, or delete a container using the DockerAPI or CLI.
* Can be run on local machines, virtual machines or deployed to the cloud.
* Is portable (can be run on any OS).
* Is isolated from other containers and runs its own software, binaries, and configurations.

When running a container, *container image* uses an isolated filesystem.This custom filesystem is provided by a container image. Since the image contains the container’s filesystem, it must contain everything needed to run an application - all dependencies, configurations, scripts, binaries, etc. The image also contains other configuration for the container, such as environment variables, a default command to run, and other metadata.

Part 2: Containerize an application
---------------------------

Build the app’s container image
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To build the container image, you’ll need to use a ``Dockerfile``. A Dockerfile is simply a text-based file with no file extension that contains a script of instructions. Docker uses this script to build a container image.

Build the container image using the following commands:

In the terminal, change directory to the ``getting-started/app`` directory. Replace ``/path/to/app`` with the path to your ``getting-started/app`` directory.

.. code-block:: console

   cd /path/to/app

Build the container image.
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: console

   docker build -t getting-started .

The ``docker build`` command uses the Dockerfile to build a new container image.

After Docker downloaded the image, the instructions from the Dockerfile copied in your application and used ``yarn`` to install your application’s dependencies. The ``CMD`` directive specifies the default command to run when starting a container from this image.

The ``-t`` flag tags your image. Think of this simply as a human-readable name for the final image. Since you named the image ``getting-started``, you can refer to that image when you run a container.

The ``.`` at the end of the ``docker build`` command tells Docker that it should look for the ``Dockerfile`` in the current directory.

Start an app container
~~~~~~~~~~~~~~~~~~~~~~

Now that you have an image, you can run the application in a container. To do so, you will use the ``docker run`` command.
1. Start your container using the ``docker run`` command and specify the name of the image you just created:

.. code-block:: console

   docker run -dp 127.0.0.1:3000:3000 getting-started

The ``-d`` flag (short for ``--detach``) runs the container in the background. The ``-p`` flag (short for ``--publish``) creates a port mapping between the host and the container. The ``-p`` flag take a string value in the format of ``HOST:CONTAINER``, where ``HOST`` is the address on the host, and ``CONTAINER`` is the port on the container. The command shown here publishes the container’s port 3000 to ``127.0.0.1:3000`` (``localhost:3000``) on the host. Without the port mapping, you wouldn’t be able to access the application from the host.


If you take a quick look at your containers, you should see at least one container running that is using the getting-started image and on port 3000. To see your containers, you can use the CLI or Docker Desktop’s graphical interface.

CLI

.. code-block:: console

   docker ps

Output similar to the following should appear.

.. code-block:: console

   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                      NAMES
   df784548666d        getting-started     "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        127.0.0.1:3000->3000/tcp   priceless_mcclintock


Docker Desktop
In Docker Desktop, select the Containers tab to see a list of your containers.

