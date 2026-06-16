stages:
  - deploy

deploy_to_server:
  stage: deploy
  image: alpine:latest
  before_script:
    # Install SSH client on the runner
    - apk add --no-cache openssh-client
    # Start SSH agent and load the private key variable
    - eval $(ssh-agent -s)
    - echo "$SSH_PRIVATE_KEY" | tr -d '\r' | ssh-add -
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
  script:
    # Securely copy (SCP) the HTML file to your Nginx web directory
    # Replace 'ubuntu' and '192.168.1.50' with your server details
    - scp -o StrictHostKeyChecking=no index.html ubuntu@192.168.1.50:/var/www/html/
  only:
    - main
