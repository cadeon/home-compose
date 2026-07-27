# Harbor Registry Setup

The bare Docker Registry (`registry.not-really.me`) is running in `service-compose.yml`.

To replace it with Harbor (which has a UI, auth, projects):

1. Stop the bare registry:
   ```
   docker compose -f service-compose.yml stop registry
   ```

2. Download the Harbor offline installer:
   ```
   wget https://github.com/goharbor/harbor/releases/download/v2.12.0/harbor-offline-installer-v2.12.0.tgz
   tar xzf harbor-offline-installer-v2.12.0.tgz
   cd harbor
   ```

3. Edit `harbor.yml`:
   ```yaml
   hostname: registry.not-really.me
   https:
     port: 443
     # Either use your own certs or let Harbor generate self-signed
     certificate: /path/to/cert
     private_key: /path/to/key
   harbor_admin_password: your-password
   data_volume: /volume2/docker-configs/harbor/data
   ```

4. Run the installer:
   ```
   ./install.sh
   ```

5. Remove the `registry` service from `service-compose.yml`.

Harbor will handle its own TLS internally (not through Traefik).
