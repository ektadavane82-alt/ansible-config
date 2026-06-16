stages:
  - deploy

# The job MUST be named 'pages' for GitLab Pages to recognize it
pages:
  stage: deploy
  image: alpine:latest  # A lightweight Linux image
  script:
    - echo "Publishing HTML artifacts..."
  artifacts:
    paths:
      - public  # Exposes the public folder to GitLab's hosting server
  only:
    - main  # Runs the pipeline only when code is pushed to the 'main' branch
