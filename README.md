# django-nested-inlines

## Overview

[Django issue #9025](http://code.djangoproject.com/ticket/9025)

The easy-to-install package from silverfix (https://github.com/silverfix/django-nested-inlines) didn't seem to work directly for Django 1.7.
There's other forks that provide some separate fixes, but none seemed to work alone,
so I just merged a couple of forks and now I can use this for my Django 1.7 project.

The installation and usage info below is copied from silverfix.

## Installation

`pip install -e git+git://github.com/oknuutti/django-nested-inlines.git#egg=django-nested-inlines`

## Usage

`nested_inlines.admin` contains three `ModelAdmin` subclasses to enable
nested inline support: `NestedModelAdmin`, `NestedStackedInline`, and
`NestedTabularInline`. To use them:

1. Add `nested_inlines` to your `INSTALLED_APPS` **before**
`django.contrib.admin`. This is because this app overrides certain admin
templates and media.
2. Import `NestedModelAdmin`, `NestedStackedInline`, and `NestedTabularInline`
wherever you want to use nested inlines.
3. On admin classes that will contain nested inlines, use `NestedModelAdmin`
rather than the standard `ModelAdmin`.
4. On inline classes, use `Nested` versions instead of the standard ones.
5. Add an `inlines = [MyInline,]` attribute to your inlines and watch the
magic happen.

## Example

	from django.contrib import admin
	from nested_inlines.admin import NestedModelAdmin, NestedStackedInline, NestedTabularInline
	from models import A, B, C
	
	class MyNestedInline(NestedTabularInline):
		model = C
	
	class MyInline(NestedStackedInline):
		model = B
		inlines = [MyNestedInline,]
	
	class MyAdmin(NestedModelAdmin):
		inlines = [MyInline,]
	
	admin.site.register(A, MyAdmin)

## Credits

This package completely the work of other developers. I've only merged their work.
Credit goes to:

- silverfix
- spanishdict
- dimoniet
- isupeene
