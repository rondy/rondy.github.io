---
layout: post
title:  "Requests specs x controller specs"
date:   2015-09-06 11:58:48
categories: software
---

# Requests specs x controller specs

* Despite of they feel to be almost the same, there is a subtle differece between them: request specs can exercice the full stack of a HTTP request (from routing to view layers).

* Request specs can also access more than one endpoint at a time, so you are able to test a whole scenario's flow, wheras in controller specs you're restrained to access only one endpoint per test case (i.e., a single controller's action).

```ruby
# request spec
specify do
  get '/my-first/enpoint'
  post '/create-some-resource'
  follow_redirect!
  get '/my-last/enpoint'
end

# controller spec
specify do
  get :new
end
```

* Given the snippet above, one could then consider requests specs for integration-test purposes (more collaboration), and controller specs for unit-test purposes (more specialization). IMHO, it would be reasonable to compare them to the parallel between feature (acceptance) specs x view specs, from a UI testing perspective.

### When to use request specs?

Whenever you need to have some level of confidence of a integration flow, mainly the ones that are not aimed to human users (i.e., there will not be interactions in the browser), or there are some routing constraint envolved (e.g., ENV var dependency, subdomain rule, etc). I also find that they're more conceptually suited for testing JSON API responses (I can expand my arguments on this last sentence later).
