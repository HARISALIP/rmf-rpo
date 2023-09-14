
# RMF Deployment Instructions

This document provides step-by-step instructions for deploying RMF (Robotics Middleware Framework) using Docker containers.

## Step 1: Install Docker

Make sure you have Docker installed on your system.

## Step 2: Run RMF Simulation

To run RMF Simulation, execute the following command:

```bash
docker run --network=host -it ghcr.io/open-rmf/rmf_deployment_template/rmf-simulation:latest bash -c "ros2 launch rmf_demos_gz office.launch.xml headless:=1 server_uri:=ws://localhost:8000/_internal"
```
## Step 3: Run RMF Web RMF Server

To run RMF Web RMF Server, execute the following command:

```bash
docker run --network=host -it ghcr.io/open-rmf/rmf_deployment_template/rmf-web-rmf-server:latest
```

## Step 4: Run RMF Web Dashboard

To run RMF Web Dashboard, execute the following command:

```bash
docker run -p 3000:80 -it ghcr.io/open-rmf/rmf_deployment_template/rmf-web-dashboard-local:latest
```

```bash
docker run -p 3000:80 -it ghcr.io/open-rmf/rmf_deployment_template/rmf-web-dashboard-local:latest
```

## Step 5: Access the Dashboard

You can now access the RMF Web Dashboard by opening your web browser and navigating to:

[http://localhost:3000/dashboard](http://localhost:3000/dashboard)

# Troubleshooting "Permission Denied" Error with Docker

If you're still encountering the "permission denied" issue even after adding your user to the `docker` group and logging out and back in, follow these steps to resolve the issue:

1. **User Session:** Make sure you've logged out completely from your user session and then logged back in. The changes to group memberships only take effect when you start a new session.

2. **Group Membership:** Verify that your user is indeed a member of the `docker` group by running the following command:

   ```bash
   groups $USER
   ```

   This command should list the groups your user belongs to, including `docker`.

3. **Docker Service:** Ensure that the Docker daemon is running. You can start or restart it with the following command:

   ```bash
   sudo systemctl start docker
   ```

4. **Docker Socket Permissions:** Check the permissions of the Docker socket file `/var/run/docker.sock` using the following command:

   ```bash
   ls -l /var/run/docker.sock
   ```

   It should typically be owned by the `docker` group. If not, you can change the ownership with the following command:

   ```bash
   sudo chown $USER:docker /var/run/docker.sock
   ```

   After changing the ownership, try running the Docker command again.

5. **Restart Your System:** As a last resort, you can try restarting your system to ensure all changes take effect.

After verifying and ensuring these steps, you should be able to run Docker commands without encountering the "permission denied" error. If the issue persists, there might be system-specific configurations or security policies affecting Docker access, and you may need to consult your system administrator or investigate those settings further.
```

You can copy and paste this Markdown text into a README.md file in your GitHub repository, and it should display properly with headings and code blocks separated as intended.
