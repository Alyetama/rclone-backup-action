# Rclone Backup Action

GitHub Action to backup your repository to any rclone-supported cloud storage service


## Requirements

Create a repository secret:

- `RCLONE_REMOTE_CONFIG`

The value of the secret variable is the content of your remote entry in the rclone config file `rclone.conf`.
Which you can find on your machine by running:

```sh
# Replace <YOUR_REMOTE_NAME> with the name of your remote
rclone config show 'REPLACE_WITH_YOUR_REMOTE_NAME' | sed -e '/^[-]/d'
```

Copy the output and use it as the value for the secret variable `RCLONE_REMOTE_CONFIG`.


## Usage

```YAML
# .github/workflows/backup.yml
name: Upload-Snapshot
on:
  push:
    branches: [ "main" ]

jobs:
  backup:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      - name: 'Create and upload snapshot'
        env:
          RCLONE_REMOTE_CONFIG: "${{ secrets.RCLONE_REMOTE_CONFIG }}"
        uses: Alyetama/rclone-backup-action@main
        with:
          config: "$RCLONE_REMOTE_CONFIG"
          remoteName: 'REPLACE_WITH_YOUR_REMOTE_NAME'
```

**Don't forget to replace `REPLACE_WITH_YOUR_REMOTE_NAME` with your remote name!**
