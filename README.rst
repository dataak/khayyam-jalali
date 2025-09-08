Khayyam
=======

A Python library for working with Jalali (Shamsi) dates and times, providing conversion, parsing, formatting, arithmetic, and comparison operations.

.. image:: http://img.shields.io/pypi/v/Khayyam-jalali.svg
     :target: https://pypi.python.org/pypi/Khayyam-jalali
.. image:: https://travis-ci.org/pylover/Khayyam-jalali.svg?branch=master
     :target: https://travis-ci.org/pylover/Khayyam-jalali
.. image:: https://img.shields.io/badge/license-GPLv3-brightgreen.svg
     :target: https://github.com/pylover/khayyam/blob/master/LICENSE
.. image:: https://pepy.tech/badge/Khayyam-jalali
     :target: https://pepy.tech/project/Khayyam-jalali
.. image:: https://pepy.tech/badge/Khayyam-jalali/month
     :target: https://pepy.tech/project/Khayyam-jalali
.. image:: https://pepy.tech/badge/Khayyam-jalali/week
     :target: https://pepy.tech/project/Khayyam-jalali

Table of Contents
^^^^^^^^^^^^^^^^^

* `Documentation <http://khayyam.dobisel.com>`_
* `Python package index <https://pypi.python.org/pypi/khayyam>`_
* `Source on github <https://github.com/pylover/khayyam>`_
* `Downloads <https://pypi.python.org/pypi/Khayyam#downloads>`_
* Basic Usage
* Current Date and Time
* Parsing & Formatting
* Converting
* Arithmetic & Operators
* Comparison
* Ordinal Functionality
* Change Log

Basic Usage
^^^^^^^^^^^

.. code-block:: python

    from khayyam import *
    JalaliDate(1346, 12, 30)
    # khayyam.JalaliDate(1346, 12, 30, Chaharshanbeh)
    JalaliDatetime(989, 3, 25, 10, 43, 23, 345453)
    # khayyam.JalaliDatetime(989, 3, 25, 10, 43, 23, 345453, Seshanbeh)

Current Date and Time
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    print(JalaliDatetime.now())
    # khayyam.JalaliDatetime(1394, 5, 18, 16, 4, 48, 628383, Yekshanbeh)
    print(JalaliDatetime.now(TehranTimezone()) - timedelta(days=6*30))
    # 1393-11-02 20:01:11.663719+03:30
    print(JalaliDate.today())
    # 1394-4-30

Parsing & Formatting
^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    print(JalaliDatetime.now().strftime('%C'))
    # شنبه ۳ مرداد ۱۳۹۴ ۰۲:۳۷:۵۲ ب.ظ
    JalaliDatetime.strptime(u'چهارشنبه ۳۱ تیر ۱۳۹۴ ۰۵:۴۵:۴۰ ب.ظ', '%C')
    # khayyam.JalaliDatetime(1394, 4, 31, 17, 45, 40, 0, Chaharshanbeh)

Converting
^^^^^^^^^^

.. code-block:: python

    from datetime import date, datetime
    JalaliDate(1394, 4, 31).todate()
    # datetime.date(2015, 7, 22)
    now = JalaliDatetime(1394, 4, 31, 15, 38, 6, 37269)
    now.todate()
    # datetime.date(2015, 7, 22)
    now.todatetime()
    # datetime.datetime(2015, 7, 22, 15, 38, 6, 37269)
    JalaliDatetime(datetime(2015, 7, 22, 14, 47, 9, 821830))
    # khayyam.JalaliDatetime(1394, 4, 31, 14, 47, 9, 821830, Chaharshanbeh)
    JalaliDatetime(datetime(2015, 7, 22, 14, 47, 9, 821830, TehranTimezone()))
    # khayyam.JalaliDatetime(1394, 4, 31, 14, 47, 9, 821830, tzinfo=+03:30 dst:60, Chaharshanbeh)
    JalaliDate(date(2015, 7, 22))
    # khayyam.JalaliDate(1394, 4, 31, Chaharshanbeh)

Arithmetic & Operators
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    from datetime import timedelta
    from khayyam import JalaliDate, JalaliDatetime
    now = JalaliDatetime(1394, 4, 31, 16, 17, 31, 374398)
    now + timedelta(days=1)
    # khayyam.JalaliDatetime(1394, 5, 1, 16, 17, 31, 374398, Panjshanbeh)
    now + timedelta(seconds=3600)
    # khayyam.JalaliDatetime(1394, 4, 31, 17, 17, 31, 374398, Chaharshanbeh)
    now - timedelta(seconds=3600)
    # khayyam.JalaliDatetime(1394, 4, 31, 15, 17, 31, 374398, Chaharshanbeh)
    yesterday = now - timedelta(1)
    yesterday
    # khayyam.JalaliDatetime(1394, 4, 30, 16, 17, 31, 374398, Seshanbeh)
    now - yesterday
    # datetime.timedelta(1)
    JalaliDatetime.now() - now
    # datetime.timedelta(0, ...)

Comparison
^^^^^^^^^^

.. code-block:: python

    now > yesterday
    # True
    now != yesterday
    # True
    now.todate() == yesterday.todate()
    # False

Ordinal Functionality
^^^^^^^^^^^^^^^^^^^^^

JalaliDate and JalaliDatetime support conversion to and from ordinal values, which represent the number of days since Farvardin 1 of year 1 (ordinal 1).

.. code-block:: python

    dt = JalaliDatetime(1395, 5, 29, 22, 18, 32)
    ordinal = dt.toordinal()
    dt_from_ordinal = JalaliDatetime.fromordinal(ordinal)
    assert dt_from_ordinal.year == dt.year
    assert dt_from_ordinal.month == dt.month
    assert dt_from_ordinal.day == dt.day
    # Time part is not preserved in ordinal, only date part is restored

Tests have been added to verify correct conversion between JalaliDatetime and ordinal values.

Change Log
^^^^^^^^^^

(See CHANGELOG file for details)
