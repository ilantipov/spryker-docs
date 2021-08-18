---
title: HowTo - Reset a Docker environment
description: Learn how to restart your Spryker in Docker from scratch.
originalLink: https://documentation.spryker.com/v6/docs/howto-reset-a-docker-environment
originalArticleId: 9ebd7c8a-d735-4bb3-8533-4c48b7ddba5d
redirect_from:
  - /v6/docs/howto-reset-a-docker-environment
  - /v6/docs/en/howto-reset-a-docker-environment
---

Sometimes, after experimenting or getting unexpected behavior from the docker/sdk up command, it may be useful to reset the entire Docker environment and start from scratch. 

{% info_block warningBox "Data removal" %}

By following the instructions below, you remove all the Docker data. 

{% endinfo_block %}

To reset a Docker environment:

1. Delete all containers, networks, unused images, and build cache:
```bash
sudo docker/sdk prune
```
2. In the project root directory, clean data, bootstrap the deploy file and start the instance:
```bash
docker/sdk clean-data && docker/sdk boot {deploy_file_name} && docker/sdk up
```

You’ve restarted your instance from scratch. 
