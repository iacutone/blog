+++
title = "filtering ack results"
date = "2016-09-15"
slug = "2016/09/15/filtering-ack-results"
Categories = []
+++

While setting up my VIM environment, I read a blogpost which states `ack` can ignore directories. For cleaner `ack` output you can setup the file below:

```bash .ackrc
--ignore-dir=log
--ignore-dir=public/assets
--ignore-dir=vendor/assets
--ignore-dir=tmp/cache
```
