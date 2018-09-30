[![CircleCI](https://circleci.com/gh/jkkitakita/circleci-danger.svg?style=svg)](https://circleci.com/gh/jkkitakita/circleci-danger)
[![](https://images.microbadger.com/badges/version/jkkitakita/circleci-danger.svg)](https://microbadger.com/images/jkkitakita/circleci-danger "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/jkkitakita/circleci-danger.svg)](https://microbadger.com/images/jkkitakita/circleci-danger "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/commit/jkkitakita/circleci-danger.svg)](https://microbadger.com/images/jkkitakita/circleci-danger "Get your own commit badge on microbadger.com")

# circleci-danger

for circleci danger

## Requirements

ruby:2.3.1-alpine

Cannot build with
- ruby:2.4.*
- ruby:2.5.*

## Docker pull

```
docker pull jkkitakita/circleci-danger
```

## Getting Started for CircleCI's setting

1. Setting up for danger to use  
https://danger.systems/guides/getting_started.html#setting-up-an-access-token
2. Setting up Contexts or Project's Environments of CircleCI for danger  
https://circleci.com/docs/2.0/contexts/
3. Add danger job to `.circleci/config.yml`

```
## Example of .circleci/config.yml

version: 2

jobs:
  danger:
    docker:
      - image: jkkitakita/circleci-danger
    steps:
      - checkout
      - run: cp ~/danger/Dangerfile .
      - run: bundle exec danger --fail-on-errors=true

workflows:
  version: 2
  danger:
    jobs:
      - danger:
        # When you use contexts
          context: danger

  # Execute periodically to update PR status
  # HACK: If create or modify of PR can be trigger it may be deleted
  scheduled-workflow:
    triggers:
      - schedule:
          cron: "0 18 * * *"
          filters:
            branches:
              ignore:
                - master
    jobs:
      - danger:
          # When you use contexts
          context: danger
```