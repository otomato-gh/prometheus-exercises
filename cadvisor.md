- Add a **CAdvisor** instance and a **redis** instance to your docker-compose file with the following snippet:
```yaml
cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor
    ports:
    - 8080:8080
    volumes:
    - /:/rootfs:ro
    - /var/run:/var/run:rw
    - /sys:/sys:ro
    - /var/lib/docker/:/var/lib/docker:ro
    depends_on:
    - redis
  redis:
    image: redis:latest
    container_name: redis
    ports:
    - 6379:6379
 ```
 
 - Add a job to scrape the cAdvisor metrics (metrics are available on port 8080)
 
 - Verify Prometheus scrapes cAdvisor by running a query in Prom Expression Browser (or Grafana Explore): `container_start_time_seconds`
 
 - Create a dashboard in Grafana to monitor memory usage per container
 
