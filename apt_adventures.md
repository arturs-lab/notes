When trying to run apt-get update via ansible, execution crashed because release info was being changed and ansible did not like that. 
Error message was
```
This must be accepted explicitly before updates for this repository can be applied. See apt-secure(8) manpage for details
```
There's a [workaround](https://github.com/ansible/ansible/issues/48352#issuecomment-808686091) to do the following in ansible
```
- name: Allow release-info to change for APT repositories
  command: apt-get update -y --allow-releaseinfo-change
  when: "'opizero2' in group_names"
```
instead of
```
- name: Update apt
  apt: update_cache=yes
```
But even doing this, execution failed. Finally, logging into the host and executing ```apt-get update --allow-releaseinfo-change``` fixed the problem.


While trying to run apt-get, I was getting errors. It appeared that apt-get was corrupt. Reinstalling it by executing ```sudo apt-get --reinstall install apt``` fixed the problem.
