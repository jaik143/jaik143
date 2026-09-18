<h1 align="center">Jayanth Kumar Kadali</h1>

<p align="center">
  <b>Cloud / DevOps Engineer</b><br>
  I build automated, scalable and secure cloud infrastructure using AWS, Kubernetes, Terraform and CI/CD.
</p>

<p align="center">
  <a href="https://linkedin.com/in/jayanth-kadali-419798182"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="mailto:jayanthk468@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
</p>

---

## About

I design, deploy and operate cloud infrastructure on AWS, with a focus on making it reproducible, observable and secure by default.

My work centres on:

- **Cloud infrastructure** — multi-AZ VPC design, subnet isolation, load balancing, auto scaling
- **Infrastructure as Code** — Terraform with remote state and state locking, composed from modules
- **CI/CD automation** — GitHub Actions and Jenkins pipelines from commit to running workload
- **Containers & orchestration** — minimal image builds, Kubernetes deployments, Helm packaging
- **DevSecOps** — static analysis and vulnerability scanning as pipeline stages, least-privilege IAM
- **Reliability & monitoring** — CloudWatch, Prometheus and Grafana, log and flow-log retention

I came to infrastructure from application development, which is why I care about the whole path from source commit to running workload rather than just the pieces at either end.

---

## Tech Stack

**Cloud**  
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white)

`EC2` · `VPC` · `EKS` · `S3` · `RDS` · `IAM` · `Lambda` · `ALB` · `Auto Scaling` · `CloudFront` · `CloudWatch` · `CloudTrail` · `DynamoDB` · `ECR`

**Infrastructure as Code**  
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)

**Containers & Orchestration**  
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white)

**CI/CD**  
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=flat-square&logo=argo&logoColor=white)

**Observability & Security**  
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=flat-square&logo=sonarqube&logoColor=white)
`Trivy` · `AWS WAF` · `VPC Flow Logs`

**Scripting & Platform**  
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

---

## Featured Engineering Projects

### [Go Web App — CI/CD to Kubernetes with GitHub Actions](https://github.com/jaik143/go-web-app-cicd)

A Go service packaged into a distroless image and shipped to Kubernetes by a four-job GitHub Actions pipeline, with Helm as the deployment interface.

**`Go`** · **`Docker`** · **`Kubernetes`** · **`Helm`** · **`GitHub Actions`** · **`Nginx Ingress`**

- Wrote a multi-stage Dockerfile that compiles a static Go binary and copies it into `gcr.io/distroless/base`, so the runtime image ships without a shell or package manager.
- Built a GitHub Actions workflow with separate `build`, `code-quality`, `push` and `update-tag` jobs — `go test ./...` and `golangci-lint` run as independent gates before any image is published.
- Closed the CI/CD loop: the pipeline writes the new image tag back into the Helm chart's `values.yaml` and commits it, so the deployed version always traces to a single build.
- Tagged every image with its workflow run ID rather than `latest`, making a rollback a Helm value change to a known-good tag instead of a rebuild.

---

### [Highly Available AWS Infrastructure with Terraform](https://github.com/jaik143/aws-infra-with-terraform)

A multi-AZ AWS environment provisioned entirely as code, with an Nginx reverse-proxy tier fronting Apache backends behind external and internal load balancers.

**`Terraform`** · **`AWS VPC`** · **`EC2`** · **`ALB`** · **`NAT Gateway`** · **`S3`** · **`DynamoDB`** · **`Nginx`**

- Provisioned a VPC spanning two availability zones with paired public/private subnets, and one NAT Gateway per AZ so a single-AZ failure does not cut egress for the surviving zone.
- Composed the estate from local Terraform modules (VPC, subnets, route tables, NAT, security groups, load balancers, EC2) instead of one flat configuration, so each layer is versioned and reusable.
- Configured an S3 remote backend with DynamoDB state locking, making concurrent `apply` runs safe for more than one operator.
- Generated Nginx configuration and EC2 user data with `templatefile()`, so proxy upstreams are derived from Terraform outputs rather than hand-edited after deploy.
- Split traffic across an external ALB at the edge and an internal ALB in front of the Apache tier, keeping backends off the public internet.

---

### [Production-Grade 3-Tier AWS Architecture](https://github.com/jaik143/AWS-3-Tier-Architecture)

A three-tier web architecture on AWS built for high availability, with the database tier fully isolated from the internet.

**`AWS VPC`** · **`EC2`** · **`ALB`** · **`Auto Scaling`** · **`RDS Multi-AZ`** · **`CloudFront`** · **`WAF`** · **`CloudWatch`**

- Built out a three-tier VPC — public web tier, private application tier, isolated database tier — where each tier accepts traffic only from the tier above it via security group references rather than CIDR ranges.
- Deployed an internet-facing ALB for the web tier and an internal ALB for the application tier, so application servers are never directly reachable.
- Ran both tiers behind Auto Scaling Groups across multiple availability zones, with RDS in Multi-AZ so losing an AZ does not take the stack down.
- Fronted the stack with CloudFront and AWS WAF for edge caching and request filtering, and wired CloudWatch alarms to SNS for alerting.

> Built on the reference architecture from the AWS three-tier web architecture workshop, deployed and extended end to end in my own account.

---

### [AWS Resource Tracker](https://github.com/jaik143/Shell-sceipting-Project)

A Bash utility that reports live AWS account usage across services, designed to run unattended as a scheduled job.

**`Bash`** · **`AWS CLI`** · **`jq`** · **`cron`** · **`Linux`**

- Queries EC2, S3, Lambda and IAM through the AWS CLI and renders a single consolidated usage report.
- Parses CLI JSON with `jq` into readable columns instead of dumping raw API responses.
- Runs under `set -euo pipefail` with a preflight check on AWS credentials, so a broken run fails loudly rather than reporting an empty account.
- Writes a dated log file so an account keeps a usage trail from cron alone, with no additional tooling.

---

### [Containerising a Django Application](https://github.com/jaik143/Conterization-of-django-application)

A Django application packaged for container-based deployment, with the image build and runtime configuration separated from the application code.

**`Docker`** · **`Python`** · **`Django`** · **`Linux`**

- Wrote a Dockerfile that installs pinned dependencies from `requirements.txt` as a distinct layer, so dependency installation is cached and only invalidated when requirements actually change.
- Bound the development server to `0.0.0.0` inside the container so it is reachable through published ports, and documented the port-mapping and host access path for both local and remote hosts.

---

<p align="center">
  <a href="https://linkedin.com/in/jayanth-kadali-419798182">LinkedIn</a> ·
  <a href="mailto:jayanthk468@gmail.com">jayanthk468@gmail.com</a>
</p>
