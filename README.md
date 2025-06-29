<p align="center">
  <a href="https://www.django-unicorn.com/"><img src="https://github.com/adamghill/django-unicorn/raw/a98539b6e4b1123705559116a77e63eea7e2b8d0/img/unicorn-logo.png" alt="django-unicorn logo" height="200"/></a>
</p>

<h1 align="center">
  <a href="https://www.django-unicorn.com/">Unicorn</a>
  <p>The magical reactive component framework for Django ✨</p>
</h1>

![PyPI](https://img.shields.io/pypi/v/django-unicorn?color=blue&style=flat-square)
![PyPI - Downloads](https://img.shields.io/pypi/dm/django-unicorn?color=blue&style=flat-square)
![coverage](https://raw.githubusercontent.com/adamghill/django-unicorn/python-coverage-comment-action-data/badge.svg)
![GitHub Sponsors](https://img.shields.io/github/sponsors/adamghill?color=blue&style=flat-square)
[![All Contributors](https://img.shields.io/badge/all_contributors-17-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE - Do not remove or modify above line -->

[Unicorn](https://www.django-unicorn.com) adds modern reactive component functionality to your Django templates without having to learn a new templating language or fight with complicated JavaScript frameworks. It seamlessly extends Django past its server-side framework roots without giving up all of its niceties or forcing you to rebuild your application. With Django Unicorn, you can quickly and easily add rich front-end interactions to your templates, all while using the power of Django.

**[https://www.django-unicorn.com](https://www.django-unicorn.com) has extensive documentation, code examples, and more!**

## ⚡ Getting started

### 1. [Install the package](https://www.django-unicorn.com/docs/installation/)

`pip install django-unicorn` OR `poetry add django-unicorn`

### 2. Add `django_unicorn` to `INSTALLED_APPS`

```python
# settings.py
INSTALLED_APPS = (
    # other apps
    "django_unicorn",
)
```

### 3. Update urls.py

```python
# urls.py
import django_unicorn

urlpatterns = (
    # other urls
    path("unicorn/", include("django_unicorn.urls")),
)
```

### 4. Add `Unicorn` to the HTML template

```html
<!-- template.html -->
{% load unicorn %}

<html>
  <head>
    {% unicorn_scripts %}
  </head>
  <body>
    {% csrf_token %}
  </body>
</html>
```

### 5. [Create a component](https://www.django-unicorn.com/docs/components/)

`python manage.py startunicorn myapp COMPONENT_NAME`

`Unicorn` uses the term "component" to refer to a set of interactive functionality that can be put into templates. A component consists of a Django HTML template and a Python view class which contains the backend code. After running the management command, two new files will be created:

- `myapp/templates/unicorn/COMPONENT_NAME.html` (component template)
- `myapp/components/COMPONENT_NAME.py` (component view)

### 6. Add the component to your template

```html
<!-- template.html -->
{% load unicorn %}

<html>
  <head>
    {% unicorn_scripts %}
  </head>
  <body>
    {% csrf_token %}

    {% unicorn 'COMPONENT_NAME' %}
  </body>
</html>
```

## [Example todo component](https://www.django-unicorn.com/examples/todo)

The `unicorn:` attributes bind the element to data and can also trigger methods by listening for events, e.g. `click`, `input`, `keydown`, etc.

```html
<!-- todo.html -->

<div>
  <form unicorn:submit.prevent="add">
    <input type="text"
      unicorn:model.defer="task"
      unicorn:keyup.escape="task=''"
      placeholder="New task" id="task"></input>
  </form>
  <button unicorn:click="add">Add</button>
  <button unicorn:click="$reset">Clear all tasks</button>

  <p>
    {% if tasks %}
      <ul>
        {% for task in tasks %}
          <li>{{ task }}</li>
        {% endfor %}
      </ul>
    {% else %}
      No tasks 🎉
    {% endif %}
  </p>
</div>
```

```python
# todo.py

from django_unicorn.components import UnicornView
from django import forms

class TodoForm(forms.Form):
    task = forms.CharField(min_length=2, max_length=20, required=True)

class TodoView(UnicornView):
    form_class = TodoForm

    task = ""
    tasks = []

    def add(self):
        if self.is_valid():
            self.tasks.append(self.task)
            self.task = ""
```

## ✨ Wait, is this magic?

Sort of! At least it might feel like it. 🤩

1. `Unicorn` progressively enhances a normal Django view, so the initial render is fast and great for SEO.
2. `Unicorn` binds to the elements you specify and automatically makes AJAX calls when needed.
3. `Unicorn` seamlessly updates the DOM when the HTML changes.

Focus on building regular Django templates and Python classes without needing to switch to another language or use unnecessary infrastructure.

## 🤯 But wait, there's more!

As if that wasn't enough, other features include:

- [Form Validation](https://www.django-unicorn.com/docs/validation/)
- [Redirection](https://www.django-unicorn.com/docs/redirecting/)
- [Loading States](https://www.django-unicorn.com/docs/loading-states/)
- [Dirty States](https://www.django-unicorn.com/docs/dirty-states/)
- [Partial Updates](https://www.django-unicorn.com/docs/partial-updates/)
- [Polling](https://www.django-unicorn.com/docs/polling/)
- [Scroll Triggering](https://www.django-unicorn.com/docs/visibility/)
- [Messages](https://www.django-unicorn.com/docs/messages/)
- [Javascript Integration](https://www.django-unicorn.com/docs/advanced/)

## 📖 Dig In

- [Documentation](https://www.django-unicorn.com/docs/)
- [Examples](https://www.django-unicorn.com/examples/todo)
- [Screencasts](https://www.django-unicorn.com/screencasts/installation)
- [Changelog](https://www.django-unicorn.com/docs/changelog/)

## ❤️ Support

This project is supported by GitHub [Sponsors](https://github.com/sponsors/adamghill) and [Digital Ocean](https://m.do.co/c/617d629f56c0).

<p>
  <a href="https://m.do.co/c/617d629f56c0">
    <img src="https://opensource.nyc3.cdn.digitaloceanspaces.com/attribution/assets/SVG/DO_Logo_horizontal_blue.svg" width="201px">
  </a>
</p>

## 🔧 Contributors

Check out [this guide](DEVELOPING.md) for more details on how to contribute.

Thanks to the following wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)) who have helped build `Unicorn`.

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->


<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
