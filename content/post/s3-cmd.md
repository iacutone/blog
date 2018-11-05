---
title: "S3 Cmd"
date: 2018-09-18T16:57:14-04:00
draft: false
---

I am a huge fan of [S3cmd](https://s3tools.org/s3cmd), a command line utility for pushing files to S3 buckets. Below is a bash script I use to push to an S3 bucket. 

```bash
#!/bin/bash
set -e

branch_name=$(git rev-parse --abbrev-ref HEAD)
if [ "$branch_name" == "master"]; then
  cp style.css build/style.css
  cp app.js build/app.js
  cp index.html build/index.html

  s3cmd sync --recursive build/ s3://<s3-bucket-name>
  echo -e "\t Successfully deployed to S3"
fi
```

First, I define a `branch_name` variable. Then, when pushing to the master branch in GitHub, a pre-push git hook pushes your changes to a S3 bucket before the changes are committed to GitHub. To try this yourself, put the above bash script in `$ touch .git/hooks/pre-push`.

I have success with this strategy along with S3 static bucket hosting for websites on AWS S3. Changes to my S3 websites auto push, leaving me with less things to do.

