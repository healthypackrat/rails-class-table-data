# rails-class-table-data

[rails-class-table-v2](https://github.com/healthypackrat/rails-class-table-v2)用のデータ(`entries.json`)を生成します。

## 生成手順

```
$ git clone https://github.com/rails/rails-dev-box.git
$ cd rails-dev-box
$ git clone https://github.com/rails/rails.git
$ vagrant up
$ vagrant ssh

(vagrant) $ cd /vagrant/rails
(vagrant) $ git checkout -b 6-0-stable origin/6-0-stable
(vagrant) $ bundle
(vagrant) $ bundle exec rake rdoc
(vagrant) $ exit

$ cd /path/to/rails-class-table-data
$ cp -R /path/to/rails-dev-box/rails/doc/rdoc tmp/v6.0.0
$ echo v6.0.0 > RAILS_VERSION
$ rake
$ cp entries.json /path/to/rails-class-table-v2/src/data
```
