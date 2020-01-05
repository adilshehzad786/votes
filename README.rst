
<h2>Option 1</h2>
<p>
<span class="code">$ pip install https://github.com/adilshehzad786/votes-2.0/zipball/master</span>
</p>

<h2>Option 2</h2>
<p>
<span class="code">$ pip install git+https://github.com/adilshehzad786/votes-2.0</span>
</p>

<h2>Option 2b</h2>
<p>
<span class="code">$ pip install git+https://github.com/adilshehzad786/votes-2.0.git</span>
</p>

<h2>Option 3</h2>
<p>
<span class="code">$ pip install -e git+https://github.com/adilshehzad786/votes-2.0.git#egg=votes-2.0</span>
</p>

<hr>

<p>
Discussed on Reddit here: <a href="http://redd.it/2crput">http://redd.it/2crput</a>.
</p>


<p class="my-span">
Options 1, 2 and 2b should give the same result. If not, it may be because of
using a local cache. The cache is in the <span class="code">$HOME/.pip</span> folder (under Linux). To avoid problems,
you can delete this folder.
</p>

<p class="my-span">
If you want to create a <span class="code">requirements.txt</span> file (with <span class="code">pip freeze --local</span>), Options
1, 2 and 2b won't reflect in <span class="code">requirements.txt</span> that the software should be
installed from GitHub. Instead, it will be downloaded from PyPi, which may
contain an older version.

Thus, if you want to include in <span class="code">requirements.txt</span> that the software should be
installed from GitHub, use Option 3.
</p>

<h3>Examples</h3>
<p>
# using Option 1<br>
<span class="code">$ pip install https://github.com/django-extensions/django-extensions/zipball/master</span><br>
<span class="code">$ pip freeze --local</span><br>
<span class="code">django-extensions==1.4.0</span><br>
</p>

<p>
# using Option 3<br>
<span class="code">$ pip install -e git+https://github.com/django-extensions/django-extensions.git#egg=django-extensions</span><br>
<span class="code">$ pip freeze --local</span><br>
<span class="code">-e git+https://github.com/django-extensions/django-extensions.git@4034b96b1879a14af3c26872e739abcad3fc4f3d#egg=django_extensions-master</span><br>
</p>

<p></p>
</div>
=============================
DRF Votes
=============================

.. image:: https://badge.fury.io/py/votes.png
    :target: https://badge.fury.io/py/votes


DRF Vote is a simple Django Rest Framework app to add ability to like/dislike a model.

Blog
-------------

You can read more about it on my blog_

.. _blog: https://medium.com/tixdo-labs/vote-your-model-with-no-pain-9d7670b65bfd#.5q8jkl7xt.

Quickstart
----------


Note
----------
    User must be logged-in to user user-specific apis.

1. Install votes::

    pip install votes




2. Add ``'votes'`` to your ``INSTALLED_APPS`` setting like this::

    INSTALLED_APPS = (
    ...
    'votes',
    )

3. Run ``python manage.py syncdb`` to create the vote models.


4. Declare vote field to the model you want to vote::

    from votes.managers import VotableManager

    class ArticleReview(models.Model):
        ...
        votes = VotableManager()

5. Include votes url to your urls.py file::

    from django.conf.urls import include
    from django.conf.urls import url

    from votes import urls

    urlpatterns += [
        url(r'^', include(urls)),
    ]

=====
DRF Vote
=====

This is extended version of repo django-vote_

.. _django-vote: https://github.com/Beeblio/django-vote

DRF Vote is a simple Django Rest Framework app to add ability to like/dislike a model.

You can read more about it on my blog post_

.. _post: https://medium.com/@3117Jain/vote-your-model-with-no-pain-9d7670b65bfd#.3zttxekr2

=====
How is it different ?
=====

- Modified to work with django rest framework.
- A new feature of disliking an object is added in this version.


APIs
-----------

/votes/up/
==========
Adds a new like or dislike vote to the object

* param: model, id, vote i.e. model=movies&id=359&vote=true
* vote=option[true for up-vote, false for down-vote, None for no-vote]

    This api is used for both liking and disliking the object.
    Send
    vote=true for like
    vote=false for dislike

/votes/down/
==========
Removes vote to the object

* param: model, id i.e. model=movies&id=359

/votes/exists/
============
Check if the user already voted the object

* param: model, id i.e. model=movies&id=359

/votes/all/
=========
return all instances voted by user

* param: model, id i.e. model=movies&id=359

/votes/count/
=======
Returns the number of votes for the object

* param: model, id i.e. model=movies&id=359

/votes/users/
=======
Returns a list of users who voted and their voting date

* param: model, id i.e. model=movies&id=359

/votes/likes/
=======
Returns the number of likes and dislikes for the object.

* param: model, id i.e. model=movies&id=359



Running Tests
--------------

Does the code actually work?

::

    source <YOURVIRTUALENV>/bin/activate
    (myenv) $ pip install -r requirements-test.txt
    (myenv) $ python runtests.py

Credits
---------

Tools used in rendering this package:

*  Cookiecutter_
*  `cookiecutter-pypackage`_

.. _Cookiecutter: https://github.com/audreyr/cookiecutter
.. _`cookiecutter-djangopackage`: https://github.com/pydanny/cookiecutter-djangopackage
