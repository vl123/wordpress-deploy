# Steps

- Generate SSH key on local machine:
  ```
  ssh-keygen -t ed25519 -f ~/.ssh/KEY_NAME -C "KEY_COMMENT"
  ```

- Add public key to `/home/USER_NAME/.ssh/authorized_keys`

- Add `SSH_HOST`, `SSH_USERNAME`, `SSH_PRIVATE_KEY`, `SSH_PASSPHRASE`, `PUBLIC_DIR`, `REPOSITORY_DIR` to GitHub secrets.

- Setup bare repository on the server:

    ```shell
    cd /private # dir outside web root
    git init --bare REPO_NAME.git
    ```

- Add `post-receive` hook to the bare repository and set `TARGET`, `GIT_DIR` and `TARGET_BRANCH`:
    ```shell
    cd REPO_NAME.git/hooks
    nano post-receive
    # Add content from post-receive file
    chmod +x post-receive
    ```

- Add `.github/workflows/deploy.yml` to the project, setup branch name and disable/enable required steps.
 
- Add `gitignore/.gitignore` to the project and modify it if necessary.
