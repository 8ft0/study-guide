### Systemd Service Management Study Sheet

**Purpose**: To provide a quick reference for managing system services using `systemd` on a Linux system.

---

#### Basic Systemd Commands

1. **Start a Service**:
   ```sh
   sudo systemctl start <service-name>
   ```

2. **Stop a Service**:
   ```sh
   sudo systemctl stop <service-name>
   ```

3. **Restart a Service**:
   ```sh
   sudo systemctl restart <service-name>
   ```

4. **Reload Service Configuration**:
   ```sh
   sudo systemctl reload <service-name>
   ```

5. **Enable a Service to Start at Boot**:
   ```sh
   sudo systemctl enable <service-name>
   ```

6. **Disable a Service from Starting at Boot**:
   ```sh
   sudo systemctl disable <service-name>
   ```

7. **Check the Status of a Service**:
   ```sh
   sudo systemctl status <service-name>
   ```

8. **List All Active Services**:
   ```sh
   sudo systemctl list-units --type=service --state=active
   ```

#### Managing Service Units

1. **View Unit Files**:
   ```sh
   sudo systemctl list-unit-files --type=service
   ```

2. **Create a Custom Service**:
      - Create a new unit file in `/etc/systemd/system/`.
      - Example: `/etc/systemd/system/my-service.service`
      ```ini
      [Unit]
      Description=My Custom Service
      After=network.target

      [Service]
      ExecStart=/usr/bin/my-service
      Restart=on-failure
      User=myuser
      Group=mygroup

      [Install]
      WantedBy=multi-user.target
      ```

3. **Reload Systemd Configuration**:
   ```sh
   sudo systemctl daemon-reload
   ```

4. **Start and Enable the Custom Service**:
   ```sh
   sudo systemctl start my-service
   sudo systemctl enable my-service
   ```

#### Service Management Examples

1. **Check the Status of the SSH Service**:
   ```sh
   sudo systemctl status ssh
   ```

2. **Restart the Network Service**:
   ```sh
   sudo systemctl restart network
   ```

3. **Enable the Apache Service to Start at Boot**:
   ```sh
   sudo systemctl enable httpd
   ```

4. **Stop and Disable the MySQL Service**:
   ```sh
   sudo systemctl stop mysqld
   sudo systemctl disable mysqld
   ```

#### Troubleshooting Systemd Services

1. **View Service Logs**:
      - Use `journalctl` to view logs for a specific service.
      ```sh
      sudo journalctl -u <service-name>
      ```
      - Example: View logs for the nginx service.
      ```sh
      sudo journalctl -u nginx
      ```

2. **Analyze Failed Services**:
      - List failed services.
      ```sh
      sudo systemctl --failed
      ```
      - Example: View details of a failed service.
      ```sh
      sudo systemctl status <failed-service-name>
      ```

3. **Debugging a Service**:
      - Run a service in debug mode.
      ```sh
      sudo systemctl edit <service-name>
      ```
      - Add the following under `[Service]`:
      ```ini
      [Service]
      Environment=SYSTEMD_LOG_LEVEL=debug
      ```

#### Useful Commands and Tips

1. **Check All Active Units**:
   ```sh
   systemctl list-units
   ```

2. **Mask a Service**:
      - Prevent a service from being started.
      ```sh
      sudo systemctl mask <service-name>
      ```

3. **Unmask a Service**:
      - Allow a previously masked service to be started.
      ```sh
      sudo systemctl unmask <service-name>
      ```

4. **Isolate a Target**:
      - Change the system state to a specific target (similar to runlevels).
      ```sh
      sudo systemctl isolate <target>
      ```

5. **Set Default Target**:
      - Set the default target to multi-user (equivalent to runlevel 3).
      ```sh
      sudo systemctl set-default multi-user.target
      ```
      - Set the default target to graphical (equivalent to runlevel 5).
      ```sh
      sudo systemctl set-default graphical.target
      ```

By using this study sheet, new starters can effectively manage system services using `systemd`, ensuring proper operation and configuration of essential system services.