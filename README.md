# Ansible tvl2386.simple_fw role

> `tvl2386.simple_fw` is an [Ansible](http://www.ansible.com) role which:
>
> * manages an iptables ruleset

## Installation

Using `ansible-galaxy`:

```shell
$ ansible-galaxy install tvl2386.simple_fw
```

Using `requirements.yml`:

```yaml
- src: tvl2386.simple_fw
```

Using `git`:

```shell
$ git clone https://github.com/tvl2386/ansible-simple_fw.git tvl2386.simple_fw
```

## Dependencies

* Ansible >= 2.0

## Usage

This is an example playbook:

```yaml
---

- hosts: all
  roles:
    - tvl2386.simple_fw
  vars:
    simple_fw_rules: |
      *mangle
      :PREROUTING ACCEPT [0:0]
      :INPUT ACCEPT [0:0]
      :FORWARD ACCEPT [0:0]
      :OUTPUT ACCEPT [0:0]
      :POSTROUTING ACCEPT [0:0]
      COMMIT
    
      *nat
      :PREROUTING ACCEPT [0:0]
      :INPUT ACCEPT [0:0]
      :OUTPUT ACCEPT [0:0]
      :POSTROUTING ACCEPT [0:0]
      COMMIT
    
      *filter
      :INPUT DROP [0:0]
      :FORWARD DROP [0:0]
      :OUTPUT DROP [0:0]
      
      # Allow return traffic
      -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
      -A OUTPUT -j ACCEPT
      COMMIT

```


## Contributing
In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests and examples for any new or changed functionality.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License
Copyright (c) TvL2386 under the MIT license.