Muffin-Session
##############

.. _description:

Muffin-Session -- Implement an user sessions in Muffin Framework.

.. _badges:

.. image:: http://img.shields.io/travis/klen/muffin-session.svg?style=flat-square
    :target: http://travis-ci.org/klen/muffin-session
    :alt: Build Status

.. image:: http://img.shields.io/pypi/v/muffin-session.svg?style=flat-square
    :target: https://pypi.python.org/pypi/muffin-session

.. image:: http://img.shields.io/pypi/dm/muffin-session.svg?style=flat-square
    :target: https://pypi.python.org/pypi/muffin-session

.. _contents:

.. contents::

.. _requirements:

Requirements
=============

- python >= 3.3

.. _installation:

Installation
=============

**Muffin-Session** should be installed using pip: ::

    pip install muffin-session

.. _usage:

Usage
=====

* Add **muffin_session** to **PLUGINS** in your Application configuration.
* Setup options if needed (see bellow).

Options
-------

`SESSION_AUTO_LOAD` -- Load session every request automatically
Session will be loaded into `request.session`.

`SESSION_DEFAULT_USER_CHECKER` -- A function which checks logged user (lambda x: x)

`SESSION_LOGIN_URL` -- Redirect URL ('/login'), or it may be a function
which accepts `request` object and returns a string.

`SESSION_SECRET` -- A secret code ('Insecuresecret')

Examples
--------

::

    @app.ps.session.user_loader
    def load_user(_id):
        """Define your own user loader. """

    @app.register('/session')
    def get_session(request):
        """ Load session and return it as JSON. """
        session = yield from app.ps.session(request)
        return dict(session)

    @app.register('/admin')
    @app.ps.session.user_pass(lambda u: u.is_admin)
    def admin(request):
        """ Check for user is admin. """


    @app.register('/login')
    def login(request):
        """ Login user. """
        # ...
        yield from app.ps.session.login(current_user.pk)


    @app.register('/logout')
        """ Logout user. """
        # ...
        yield from app.ps.session.logout(curuser.pk)


.. _bugtracker:

Bug tracker
===========

If you have any suggestions, bug reports or
annoyances please report them to the issue tracker
at https://github.com/klen/muffin-session/issues

.. _contributing:

Contributing
============

Development of Muffin-Session happens at: https://github.com/klen/muffin-session


Contributors
=============

* klen_ (Kirill Klenov)

.. _license:

License
=======

Licensed under a `MIT license`_.

If you wish to express your appreciation for the project, you are welcome to send
a postcard to: ::

    Kirill Klenov
    pos. Severny 8-3
    MO, Istra, 143500
    Russia

.. _links:


.. _klen: https://github.com/klen

.. _MIT license: http://opensource.org/licenses/MIT
