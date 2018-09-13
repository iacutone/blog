---
title: "Rails Helper Method"
date: 2018-09-13T10:51:44-04:00
draft: false
slug = "rails-helper"
tags:
- Ruby
- Rails
---

Helper methods allow controller methods to be called in the associated layout code.

```ruby
  # UserController

  helper_method def current_user
    @current_user ||= User.find(params[:id])
  end
```

```html
  # User Show Page

  <h1>Hello, <%= current_user %></h1>
```

### Why use a `helper_method`?

A helper method is advantageous to use over an instance variable in a variety of ways.

1. Instance variable value is set to `nil` which can lead to unexpected results

```ruby
  def test
    @test
  end

  # test == nil
```

1. Instance variables are more difficult to maintain due to tracking of read and write, especially when `@object` is used in many places

1. Helper methods can return a more useful stack trace

1. Helper methods keep controller actions DRY

```ruby
  def edit
  end

  def update
  end

  def show
  end

  helper_method def active_record_object
    @object ||= ActiveRecordObject.find(params[:id])
  end
```

I recommend replacing instance method calls with `helper_method`'s in your Rails code!
