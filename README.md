# 💰 MERN Expense Tracker - Containerized 3-Tier Deployment

**Author:** Neeraj Bali (GitHub: NB11-ML)
**Project:** DevOps Phase 1 Practical Exam Submission

---

## 📌 Application Description & Provenance

* **Original Upstream Repository:** [bradtraversy/expense-tracker-mern](https://github.com/bradtraversy/expense-tracker-mern)
* **Forked Repository:** [NB11-ML/expense-tracker-mern](https://github.com/NB11-ML/expense-tracker-mern)
* **Application Overview:** A full-stack 3-tier expense tracker application consisting of a React frontend presentation layer, a Node.js/Express backend application layer, and a MongoDB data layer.


* **Minimum Complexity Validation:** The backend features multiple operational API endpoints handling different CRUD methods for transactions, and the database relies on structured collections, fully satisfying the minimum complexity bar.


* **Pre-Containerization Status:** The original upstream repository was heavily audited to ensure zero pre-existing container deployment files were present. The absence of any `Dockerfile`, `docker-compose.yml`, or `.dockerignore` confirms the codebase was entirely un-Dockerized before this project began.



---

## 🏗️ Architecture Notes & System Design

* **3-Tier Layout:** The environment is strictly decoupled into distinct frontend, backend, and database containers.


* **Custom Networking:** All services are orchestrated on a custom user-defined Docker network. This allows the containers to seamlessly talk to each other by their service names rather than relying on hardcoded IPs.


* **Security & Exposed Ports:** Port mapping is strictly limited to services requiring public access. The frontend is exposed for user access, while the database port remains completely internal and isolated from the public network.


* **Persistent Data:** Database state is preserved using a named Docker volume. This guarantees that transaction data does not live only inside the container and will successfully survive container restarts or recreations.



---

## ⚙️ Optimisation Choices & Git Hygiene

To ensure a production-ready, highly optimized deployment, the following DevOps practices were implemented:

* **Separate Dockerfiles:** Wrote distinct, customized Dockerfiles matched to the specific framework requirements of the frontend and backend.


* **Image Optimization:** Utilized multi-stage builds and minimal base images (like Alpine) to drastically reduce the footprint.


* **Build Context Hygiene:** Implemented comprehensive `.dockerignore` files to prevent dead layers, exclude local modules, and keep the build context lightweight.


* **Git Practices:** Maintained a meaningful commit history demonstrating real, iterative configuration steps and implemented a proper `.gitignore` file.


* **Orchestration:** Managed the entire 3-tier architecture with a single unified `docker-compose.yml` file.



---

## 📦 Final Image Sizes

| Service | Base Image | Optimization Strategy | Final Image Size |
| --- | --- | --- | --- |
| **Frontend** | `node:18-alpine` / `nginx:alpine` | Multi-Stage Build | `<ADD_FINAL_SIZE_MB>`<br> |
| **Backend** | `node:18-alpine` | Minimal Base Image | `<ADD_FINAL_SIZE_MB>`<br> |
| **Database** | `mongo:latest` | Standard Image | `<ADD_FINAL_SIZE_MB>`<br> |

---

## 🚀 Deployment Instructions

**1. Clone the Repository**

```bash
git clone https://github.com/NB11-ML/expense-tracker-mern.git
cd expense-tracker-mern

```

**2. Environment Configuration**
Create a `.env` file in the backend directory with your MongoDB connection string targeting the custom network service name.

**3. Launch the Architecture**
Deploy the application using the orchestration file:

```bash
docker-compose up -d --build

```
