## Manages the Application on Kubernetes

Running differnet web application on K8s
Different guides for running microservices in Kubernetes.

Specifications:

* Release automation (Make/TravisCI/CircleCI/Quay.io/Google Cloud Container Builder/Skaffold/Weave Flux)
* Multi-platform Docker image (amd64/arm/arm64/ppc64le/s390x)
* Health checks (readiness and liveness)
* Graceful shutdown on interrupt signals
* File watcher for secrets and configmaps
* Instrumented with Prometheus
* Tracing with Istio and Jaeger
* Structured logging with zap
* 12-factor app with viper
* Fault injection (random errors and latency)
* Helm chart

Web API:

* `GET /` prints runtime information
* `GET /version` prints podinfo version and git commit hash
* `GET /metrics` return HTTP requests duration and Go runtime metrics
* `GET /healthz` used by Kubernetes liveness probe
* `GET /readyz` used by Kubernetes readiness probe
* `POST /readyz/enable` signals the Kubernetes LB that this instance is ready to receive traffic
* `POST /readyz/disable` signals the Kubernetes LB to stop sending requests to this instance
* `GET /status/{code}` returns the status code
* `GET /panic` crashes the process with exit code 255
* `POST /echo` forwards the call to the backend service and echos the posted content
* `GET /env` returns the environment variables as a JSON array
* `GET /headers` returns a JSON with the request HTTP headers
* `GET /delay/{seconds}` waits for the specified period
* `POST /token` issues a JWT token valid for one minute `JWT=$(curl -sd 'anon' podinfo:9898/token | jq -r .token)`
* `GET /token/validate` validates the JWT token `curl -H "Authorization: Bearer $JWT" podinfo:9898/token/validate`
* `GET /configs` returns a JSON with configmaps and/or secrets mounted in the `config` volume
* `POST /store` writes the posted content to disk at /data/hash and returns the SHA1 hash of the content
* `GET /store/{hash}` returns the content of the file /data/hash if exists
* `GET /ws/echo` echos content via websockets `podcli ws ws://localhost:9898/ws/echo`
* `GET /chunked/{seconds}` uses `transfer-encoding` type `chunked` to give a partial response and then waits for the specified period

### Guides

* [Deploy and upgrade with Helm](docs/1-deploy.md)
* [Horizontal Pod Auto-scaling](docs/2-autoscaling.md)
* [Monitoring and alerting with Prometheus](docs/3-monitoring.md)
* [StatefulSets with local persistent volumes](docs/4-statefulsets.md)
* [Expose Kubernetes services over HTTPS with Ngrok](docs/6-ngrok.md)
* [A/B Testing with Ambassador API Gateway](docs/5-canary.md)
* [Canary Deployments with Istio](docs/7-istio.md)
* [GitHub Actions CI demo](docs/8-gh-actions.md)

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
