# Project Deployment Overview

## Links
- **Frontend:** [http://52.66.21.23:81/](http://52.66.21.23:81/)
- **Backend:** [http://52.66.21.23:8000/](http://52.66.21.23:8000/)

## Deployment Stack
- **Docker**: Used for containerizing the application (frontend & backend).
- **Nginx**: Configured as a reverse proxy to route traffic efficiently.
- **PostgreSQL/MongoDB**: (If applicable) Used as the database.
- **Redis**: (If applicable) Used for caching and message queuing.
- **Node.js & Express**: Backend framework.

## Infrastructure Details
- **Server**: Hosted on an AWS EC2 instance.
- **Port Mapping**:
  - Frontend runs on port `81`.
  - Backend runs on port `8000`.
  - Nginx handles the routing and load balancing.

## Deployment Process
1. Clone the repository and navigate to the project directory.
2. Use Docker Compose to build and start services:
   ```sh
   docker-compose up -d --build
   ```
3. Ensure Nginx is properly configured and restarted:
   ```sh
   systemctl restart nginx
   ```
4. Verify that both frontend and backend are accessible via their respective URLs.

## Nginx Configuration (Example)
```nginx
server {
    listen 81;
    location / {
        proxy_pass http://frontend_container:3000;
    }
}

server {
    listen 8000;
    location / {
        proxy_pass http://backend_container:8000;
    }
}
```

## Monitoring & Logs
- Use `docker logs <container_id>` to check logs.
- Ensure proper monitoring using Prometheus, Grafana, or CloudWatch.

## CI/CD Pipeline (Optional)
- Integrated with Jenkins/GitHub Actions for automated builds and deployments.
- Runs linting, tests, and Docker image builds before pushing to production.

## Security & Best Practices
- SSL termination via Nginx (if using HTTPS).
- Use `.env` for sensitive configurations and avoid hardcoding credentials.
- Regular security patching and vulnerability scanning for containers.

---

This setup ensures scalability, security, and efficient traffic handling. 🚀

