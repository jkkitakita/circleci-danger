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

1. Setting up for danger to use with CircleCI  
https://danger.systems/guides/getting_started.html#setting-up-an-access-token  
ex. Add `DANGER_GITHUB_API_TOKEN` to Project's Environments or Contexts  
cf. CircleCI 2.0 - Contexts
https://circleci.com/docs/2.0/contexts/

2. Add danger job to `.circleci/config.yml`

```
## Example of .circleci/config.yml

version: 2

jobs:
  danger:
    docker:
      - image: jkkitakita/circleci-danger
    steps:
      - checkout
      - run: cp -f ~/danger/Dangerfile .
      - run: bundle exec danger --fail-on-errors=true

workflows:
  version: 2
  danger:
    jobs:
      - danger
      # When you use contexts
      # - danger:
      #     context: danger
```