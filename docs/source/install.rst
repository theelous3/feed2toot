How to install Feed2toot
========================
From PyPI
^^^^^^^^^
    $ python -m venv .venv
    $ source .venv/bin/activate  # Windows: .venv\Scripts\activate
    (.venv) $ pip install feed2toot-oauth

From sources
^^^^^^^^^^^^
* You need Python 3.7+ with ``pip`` available.

* Clone the repository and install in editable mode for development and improved configurability::

    $ git clone https://github.com/theelous3/feed2toot-oauth.git
    $ cd feed2toot-oauth
    $ python -m venv .venv
    $ source .venv/bin/activate  # Windows: .venv\Scripts\activate
    (.venv) $ pip install -e .

  This exposes the CLI entry points ``feed2toot`` and ``feed2toot-register-app`` directly from your virtualenv.
