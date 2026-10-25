# GCP SecOps Automation: IAM Security Auditor & DevOps Pipeline

[![GCP](https://img.shields.io/badge/Google_Cloud-4285F4?style=flat&logo=google-cloud&logoColor=white)](https://cloud.google.com/)
[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)](https://jupyter.org/)

An automated **DevOps and Cloud Security (SecOps)** pipeline implemented in Python and executed via Jupyter Notebook (`.ipynb`). This project demonstrates how to dynamically manage Google Cloud Platform (GCP) resources, automate security compliance checks, and detect dangerous IAM misconfigurations—such as overly permissive roles or public exposure risks—without relying on hardcoded credentials or fixed project IDs.

---

## 🛠️ Tech Stack & Concepts

* **Cloud Provider:** Google Cloud Platform (GCP)
* **Language:** Python 3.9+
* **Interfaces:** Jupyter Notebook / Google Colab, `gcloud` CLI
* **GCP Libraries:** `google-api-python-client`, `google-auth`, `google-cloud-resourcemanager`
* **DevOps Focus:** Automated API enablement, dynamic project context retrieval, repeatable pipeline execution.
* **Security Focus:** Least-privilege IAM enforcement, public exposure detection (`allUsers`), primitive role auditing (`roles/owner`).

---

## 🏗️ Architecture & Workflow

```text
  [ JUPYTER NOTEBOOK / IPYNB ]
               │
               ▼
  ┌──────────────────────────┐
  │ Dynamic Environment Check│ ──► Retrieves active PROJECT_ID via gcloud / Env
  └────────────┬─────────────┘
               │
               ▼
  ┌──────────────────────────┐
  │ DevOps Enablement Phase  │ ──► Programmatically enables required APIs
  └────────────┬─────────────┘     (ResourceManager, IAM, Asset API)
               │
               ▼
  ┌──────────────────────────┐
  │ Cloud Security Audit     │ ──► Scans IAM Policies for:
  └────────────┬─────────────┘      • Public bindings (allUsers)
               │                    • Broad primitive roles (Owner/Editor)
               ▼
  [ SECURITY FINDINGS & REPORT ]
```

---

## 🚀 Quick Start & Setup

### Prerequisites

1. A Google Cloud Platform (GCP) Account.
2. The Google Cloud SDK (`gcloud` CLI) installed locally.
3. Python 3.9+ installed along with Jupyter Notebook or Google Colab.

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/gcp-secops-automation.git
cd gcp-secops-automation
```

### 2. Authenticate with Google Cloud

Ensure your local environment is authenticated with Application Default Credentials (ADC) and set up with your active project:

```bash
# Log in to GCP
gcloud auth login

# Set application default credentials for Python SDKs
gcloud auth application-default login

# (Optional) Set your active default project
gcloud config set project YOUR_PROJECT_ID
```

### 3. Install Python Dependencies

```bash
pip install -r requirements.txt
```

---

## 📁 Repository Structure

```text
.
├── gcp_secops_pipeline.ipynb   # Main Jupyter Notebook containing code & docs
├── README.md                   # Project documentation
└── requirements.txt            # Python dependency list
```

---

## ⚙️ How to Run

1. Launch Jupyter Notebook or Jupyter Lab:
   ```bash
   jupyter notebook
   ```
2. Open `gcp_secops_pipeline.ipynb`.
3. Run the cells sequentially from top to bottom.
4. The notebook will automatically fetch your active project context, enable necessary cloud services, perform the IAM security audit, and display findings in real time.

---

## 🔒 Security Best Practices Implemented

* **Zero Hardcoded Secrets:** Credentials and project configurations are dynamically inherited from environment variables and `gcloud` context.
* **Least Privilege Verification:** Proactively identifies where excessive access permissions exist before potential exploitation.
* **Automated Guardrails:** Scriptable logic allows easy integration into continuous integration (CI/CD) pipelines.
