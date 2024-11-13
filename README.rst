===================
docker-build-action
===================
This is a generic `GitHub Actions`_ configuration for building
`Docker`_ images. I tend to use the official Docker `build-push-action`_
in a specific way: with caching, also with build and push split into
separate steps. Following DRY principle, I factored out these common steps
into more generic composite action. It's meant primarily for my own use,
but if anyone else finds it useful - feel free to use it with your own
workflows.

Usage
=====
::

  name: docker-build-action example
  on:
    push:
      branches:
        - master
  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        # You must handle login yourself
        - name: Log in to Docker Hub
          uses: docker/login-action@master
          with:
            username: dockerhubid
            password: ${{ secrets.DOCKERHUB_TOKEN }}
        - name: Build Docker image
          uses: hbielenia/docker-build-action
          with:
            tags: dockerhubid/your-image:latest

Inputs
======
All inputs are strings.

+------------+-----------+------------------+-----------------------------------------------------------------------------------+
| Name       | Required? | Default          | Description                                                                       |
+============+===========+==================+===================================================================================+
| tags       | **yes**   | none             | Tags to use with the resulting image; multiple tags should be separated by commas.|
+------------+-----------+------------------+-----------------------------------------------------------------------------------+
| dockerfile | no        | ``'Dockerfile'`` | Path to Dockerfile.                                                               |
+------------+-----------+------------------+-----------------------------------------------------------------------------------+
| from_cache | no        | ``'0'``          | Set to ``1`` if image is already built and should be taken from cache.            |
+------------+-----------+------------------+-----------------------------------------------------------------------------------+
| push       | no        | ``'0'``          | Set to ``1`` if image should be pushed to Docker registry.                        |
+------------+-----------+------------------+-----------------------------------------------------------------------------------+

Outputs
=======
This action has no outputs on it's own.

Issues and support
==================
Bug reports and feature requests are collected at `GitHub Issues`_.
For questions and usage help, please use `Discussions`_ instead. Bear in mind
that this project isn't a full time job and no one is under any obligation
to answer. However, there is genuine intent of providing support on a
best effort basis.

Copyright
=========
This configuration isn't very original, but in case it's copyrightable
now or in the future, in whole or in part, it's released under the terms
of `CC0 1.0 Universal`_ license. This license is pretty much the same as
public domain, but adjusted for countries where author can't simply release
into public domain. See ``COPYING.txt`` for full license text.

.. _GitHub Actions: https://docs.github.com/en/actions
.. _Docker: https://docs.docker.com/get-started/docker-overview/
.. _build-push-action: https://github.com/docker/build-push-action
.. _GitHub Issues: https://github.com/hbielenia/docker-pypa-build/issues
.. _Discussions: https://github.com/hbielenia/docker-pypa-build/discussions
.. _CC0 1.0 Universal: https://creativecommons.org/publicdomain/zero/1.0/
