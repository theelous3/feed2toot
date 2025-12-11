Use Feed2toot
==============
After the configuration of Feed2toot, launch the following command from your virtual environment::

    (.venv) $ feed2toot -c /path/to/feed2toot.ini

Run Feed2toot on a regular basis
--------------------------------
Feed2toot should be launched on a regular basis in order to efficiently send your new RSS entries to Mastodon. Ensure your cron job uses the virtual environment’s binary (absolute path), for example::

    @hourly /home/johndoe/feed2toot-oauth/.venv/bin/feed2toot -c /path/to/feed2toot.ini

will execute feed2toot every hour. Or without the syntactic sugar in the global crontab file /etc/crontab::

    0 * * * * johndoe /home/johndoe/feed2toot-oauth/.venv/bin/feed2toot -c /path/to/feed2toot.ini

Test option
-----------
In order to know what's going to be sent to Mastodon without actually doing it, use the **--dry-run** option::

    $ feed2toot --dry-run -c /path/to/feed2toot.ini

Debug option
------------
In order to increase the verbosity of what Feed2toot is doing, use the **--debug** option followed by the level of verbosity see `the available different levels <https://docs.python.org/3/library/logging.html>`_::

    $ feed2toot --debug -c /path/to/feed2toot.ini

Populate the cache file without posting toots
---------------------------------------------
Feed2toot offers the **--populate-cache** command line option to populate the cache file without posting to Mastodon::

    $ feed2toot --populate-cache -c feed2toot.ini
    populating RSS entry https://www.journalduhacker.net/s/65krkk
    populating RSS entry https://www.journalduhacker.net/s/co2es0
    populating RSS entry https://www.journalduhacker.net/s/la2ihl
    populating RSS entry https://www.journalduhacker.net/s/stfwtx
    populating RSS entry https://www.journalduhacker.net/s/qq1wte
    populating RSS entry https://www.journalduhacker.net/s/y8mzrp
    populating RSS entry https://www.journalduhacker.net/s/ozjqv0
    populating RSS entry https://www.journalduhacker.net/s/6ev8jz
    populating RSS entry https://www.journalduhacker.net/s/gezvnv
    populating RSS entry https://www.journalduhacker.net/s/lqswmz

How to display available sections of the rss feed
-------------------------------------------------
Feed2toot offers the **--rss-sections** command line option to display the available section of the rss feed and exit::

    $ feed2toot --rss-sections -c feed2toot.ini
    The following sections are available in this RSS feed: ['title', 'comments', 'authors', 'link', 'author', 'summary', 'links', 'tags', id', 'author_detail', 'published'].

Using syslog
------------
Feed2toot is able to send its log to syslog. You can use it with the following command::

    $ feed2toot --syslog=WARN -c /path/to/feed2toot.ini

Limit number of rss entries published at each execution
-------------------------------------------------------
If you want to limit the number of rss entries published at each execution, you can use the --limit CLI option.

    $ feed2toot --limit 5 -c /path/to/feed2toot.ini

The number of posts to Mastodon will be at 5 posts top with this CLI option.

Use feed2toot-register-app
==========================
You need a Mastodon app associated to a user on the Mastodon instance. The script ``feed2toot-register-app`` will create an app for Feed2toot and upload it on the specified Mastodon instance using the OAuth authorization code flow.

Primary usage ::

    $ feed2toot-register-app

Possible CLI options:

- use **-c/--client** to change the filename in which the client credentials are stored (defaults to ``feed2toot_clientcred.secret``)
- use **-u/--user** to change the filename in which the user credentials are stored (defaults to ``feed2toot_usercred.secret``)
- use **-n/--name** to change the Mastodon app name (defaults to ``feed2toot``)

Example with full options and full output::

    $ feed2toot-register-app --user f2tusercreds.secret --client f2tclientcreds.secret --name f2t

    Creating application on instance...
    App registered and client credentials written to /home/me/feed2toot/creds/f2tclientcreds.secret
    Generating OAuth authorization URL...
    Open this URL in a browser, log in, and authorize the app:
    https://framapiaf.org/oauth/authorize?...
    Paste the code shown by the instance here: ABCDEFG123456
    User credentials written to /home/me/feed2toot/creds/f2tusercreds.secret

The script writes files under ``./creds`` unless you provide another path in the filenames you pass to ``--client`` or ``--user``.
