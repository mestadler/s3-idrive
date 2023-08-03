Certainly! To rename the systemd service to "s3-idrive," follow the steps below:

1. Rename the service unit file:

Open a terminal and use a text editor to rename the service unit file from "mount-s3-bitbucket.service" to "s3-idrive.service":

```bash
sudo mv /etc/systemd/system/mount-s3-bitbucket.service /etc/systemd/system/s3-idrive.service
```

2. Edit the service unit file:

```bash
sudo nano /etc/systemd/system/s3-idrive.service
```

3. Update the content of the file to match the new service name:

```ini
[Unit]
Description=Mount S3 bucket at boot time
After=network-online.target

[Service]
Type=oneshot
RemainAfterExit=true
TimeoutStartSec=20
ExecStartPre=/bin/mkdir -p /mnt/s3-bitbucket
ExecStart=/usr/bin/s3fs bitbucket /mnt/s3-bitbucket -o passwd_file=/path/to/.passwd-s3fs -o url=https://c2i0.ldn.idrivee2-22.com

[Install]
WantedBy=multi-user.target
```

Make sure to replace `/path/to/.passwd-s3fs` with the correct path to your AWS credentials file.

4. Save and close the file.

5. Reload systemd to recognize the updated service:

```bash
sudo systemctl daemon-reload
```

6. Enable the new service:

```bash
sudo systemctl enable s3-idrive.service
```

Now, your S3 bucket will be mounted automatically during the boot process using the service named "s3-idrive." If you need to check the logs for this service, you can use the following command:

```bash
sudo journalctl -u s3-idrive.service
```
