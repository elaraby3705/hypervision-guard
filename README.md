# HyperVision Guard: Intelligent Behavioral Surveillance System

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Python Version](https://img.shields.io/badge/python-3.11%2B-blue)
![Django Version](https://img.shields.io/badge/django-5.0-green)
![License](https://img.shields.io/badge/license-Proprietary-red)

## 📖 Overview

**HyperVision Guard** is an enterprise-grade surveillance orchestration system designed to manage security for large-scale facilities (e.g., Hypermarkets with 2000+ cameras). Unlike traditional CCTV systems that rely solely on passive recording, HyperVision utilizes distributed **Edge AI** to detect specific behavioral threats in real-time.

The system is architected to handle high-throughput event ingestion, real-time alert broadcasting via WebSockets, and long-term incident analysis.

### Key Capabilities
* **Product Tampering Detection:** Identifies unauthorized opening of products or aggressive handling on shelves.
* **Theft Behavior Analysis:** Detects concealment gestures (e.g., hiding items in pockets/bags) rather than just motion.
* **High-Threat Prevention:** Instantly flags weapons or aggressive body language (e.g., hold-up scenarios) with critical priority.

---

## 🏗 System Architecture

The system follows an **Event-Driven Microservices** pattern to ensure scalability and low latency.

1.  **Perception Layer (Edge):** AI models (YOLOv8/Pose Estimation) run on edge nodes, processing raw video streams locally.
2.  **Transport Layer:** Metadata and event snapshots are sent to the central core via Message Brokers (RabbitMQ/Kafka).
3.  **Core Application (This Repo):** A Django-based backend that digests events, manages state, and triggers workflows.
4.  **Presentation Layer:** A Real-time Dashboard for security personnel powered by WebSockets.

---

## 🛠 Tech Stack

* **Backend Framework:** Python / Django & Django REST Framework (DRF)
* **Real-time Communication:** Django Channels (ASGI) with Redis
* **Database:** PostgreSQL (Relational Data & TimescaleDB extensions recommended)
* **Task Queue:** Celery (for background processing & reporting)
* **Message Broker:** RabbitMQ
* **Containerization:** Docker & Docker Compose
* **Orchestration:** Kubernetes (K8s) - *Planned for Production*

---

## 🚀 Local Development Setup

### Prerequisites
* Docker & Docker Compose
* Python 3.11+
* Git

### Installation Steps

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/your-username/hypervision-guard.git](https://github.com/your-username/hypervision-guard.git)
    cd hypervision-guard
    ```

2.  **Environment Setup**
    Create a `.env` file based on the example:
    ```bash
    cp .env.example .env
    ```

3.  **Build and Run via Docker**
    ```bash
    docker-compose up --build
    ```

4.  **Apply Migrations**
    ```bash
    docker-compose exec web python manage.py migrate
    ```

5.  **Create Superuser**
    ```bash
    docker-compose exec web python manage.py createsuperuser
    ```

6.  **Access the Dashboard**
    * API Root: `http://localhost:8000/api/v1/`
    * Admin Panel: `http://localhost:8000/admin/`

---

## 📡 API Endpoints (Preview)

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/v1/ingest/event/` | Receiver for Edge AI alerts (JSON payload) |
| `GET` | `/api/v1/cameras/` | List all registered cameras and their status |
| `GET` | `/api/v1/incidents/active/` | Fetch currently unresolved security incidents |

---

## 🤝 Contribution Guidelines

1.  **Branching Strategy:** Use `feature/` for new features and `fix/` for bugs.
2.  **Commit Messages:** Follow Conventional Commits (e.g., `feat: add weapon detection model`).
3.  **Testing:** Ensure all new endpoints have coverage in `tests/`.

---

## 📄 License
Confidential & Proprietary. Unauthorized copying of this file, via any medium is strictly prohibited.
