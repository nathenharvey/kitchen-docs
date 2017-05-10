---
title: Adding a Suite
---

##### Adding a Suite

We're going to call our new Test Kitchen Suite `"server"` by opening `.kitchen.yml` in your editor of choice so that it looks similar to:

~~~
---
driver:
  name: vagrant

provisioner:
  name: chef_zero
  require_chef_omnibus: 13

verifier:
  name: inspec

platforms:
  - name: ubuntu-16.04
  - name: centos-7.3

suites:
  - name: default
    run_list:
      - recipe[git_cookbook::default]
    verifier:
      inspec_tests:
        - test/smoke/default
    attributes:
  - name: server
    run_list:
      - recipe[git_cookbook::server]
    verifier:
      inspec_tests:
        - test/smoke/server
    attributes:
~~~

Now run `kitchen list` to see our new suite in action:

~~~
$ kitchen list
Instance             Driver   Provisioner  Verifier  Transport  Last Action    Last Error
default-ubuntu-1604  Vagrant  ChefZero     Inspec    Ssh        <Not Created>  <None>
default-centos-73    Vagrant  ChefZero     Inspec    Ssh        <Not Created>  <None>
server-ubuntu-1604   Vagrant  ChefZero     Inspec    Ssh        <Not Created>  <None>
server-centos-73     Vagrant  ChefZero     Inspec    Ssh        <Not Created>  <None>
~~~

Woah, we've doubled our number of instances! Yes, that is going to happen. This explosion of test cases is just one reason why testing is hard.

<div class="sidebar--footer">
<a class="button primary-cta" href="adding-test">Next - Adding a Test</a>
<a class="sidebar--footer--back" href="adding-feature">Back to previous step</a>
</div>