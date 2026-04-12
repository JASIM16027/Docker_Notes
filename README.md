
---

## DevOps Learning Roadmap (বাংলায়)

---

### ধাপ ১ — Linux & Networking ভিত্তি
সবকিছুর শুরু এখান থেকে

- **Linux Command Line** — ফাইল সিস্টেম, পারমিশন, প্রসেস ম্যানেজমেন্ট, bash scripting
- **Networking Basics** — IP, DNS, HTTP/HTTPS, TCP/UDP, Load Balancer, Firewall
- **Git & Version Control** — Git workflow, branching, merging, GitHub/GitLab

---

### ধাপ ২ — Docker (কন্টেইনার)
১–২ মাস | সবচেয়ে গুরুত্বপূর্ণ টুল

- **Docker কী ও কেন?** — Container vs VM, image vs container, Docker Hub
- **Dockerfile লেখা** — FROM, RUN, COPY, EXPOSE, CMD — layer concept
- **Docker Compose** — Multi-container apps, volumes, networks, environment variables
- **Networking & Volumes** — Bridge, host, overlay network; bind mount vs named volume

---

### ধাপ ৩ — CI/CD Pipeline
Automation শেখার সময়

- **CI/CD ধারণা** — Build → Test → Deploy pipeline এর concept
- **GitHub Actions** — Workflows, jobs, steps, triggers, secrets
- **Jenkins (Optional)** — Jenkinsfile, pipeline as code, plugins

---

### ধাপ ৪ — AWS (Cloud Platform)
২–৩ মাস | চাকরির মূল দক্ষতা

- **Core AWS Services** — EC2, S3, IAM, VPC, RDS, Route53
- **ECS & ECR (Container)** — Docker image → ECR → ECS Fargate deploy
- **Lambda & Serverless** — Function as a service, event-driven, API Gateway
- **Monitoring & Logging** — CloudWatch, CloudTrail, alarms, dashboards

---

### ধাপ ৫ — Terraform (Infrastructure as Code)
Cloud resource code দিয়ে বানানো

- **Terraform মূল ধারণা** — Provider, resource, state, plan, apply, destroy
- **AWS + Terraform** — EC2, VPC, Security Groups, S3 কোড দিয়ে তৈরি
- **Modules & Best Practices** — Reusable modules, remote state, workspaces

---

### ধাপ ৬ — Kubernetes / K8s
৩–৪ মাস | সবচেয়ে কঠিন কিন্তু সবচেয়ে চাহিদাসম্পন্ন

- **K8s Architecture** — Master node, worker node, etcd, API server, scheduler
- **Core Objects** — Pod, ReplicaSet, Deployment, Service, ConfigMap, Secret
- **AWS EKS** — Managed Kubernetes on AWS, node groups, IAM roles
- **Helm Charts** — Package manager for K8s, templates, values, releases
- **Monitoring: Prometheus & Grafana** — Metrics, alerts, dashboards, service mesh

---

### 🎯 মোট সময়সীমা: ৮–১২ মাস

**শেখার ক্রম:** Linux → Git → Docker → CI/CD → AWS → Terraform → Kubernetes

প্রতিটি ধাপ শেষে একটা real project বানাও। তাহলে concept শক্ত হবে এবং portfolio তৈরি হবে।
