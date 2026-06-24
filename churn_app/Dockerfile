# ── Base image ──────────────────────────────────────────────────
FROM python:3.11-slim

# ── Metadata ────────────────────────────────────────────────────
LABEL maintainer="your-name"
LABEL description="Telco Churn Prediction Streamlit Dashboard"

# ── Set working directory ────────────────────────────────────────
WORKDIR /app

# ── Install system deps (for openpyxl / matplotlib) ─────────────
RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# ── Copy requirements first (layer caching) ─────────────────────
COPY requirements.txt .

# ── Install Python dependencies ──────────────────────────────────
RUN pip install --no-cache-dir -r requirements.txt

# ── Copy app source ──────────────────────────────────────────────
COPY app.py .

# ── (Optional) Copy dataset if you want it pre-loaded ───────────
# COPY Telco_customer_churn.xlsx .

# ── Expose Streamlit default port ────────────────────────────────
EXPOSE 8501

# ── Healthcheck ──────────────────────────────────────────────────
HEALTHCHECK CMD curl --fail http://localhost:8501/_stcore/health || exit 1

# ── Run the app ──────────────────────────────────────────────────
ENTRYPOINT ["streamlit", "run", "app.py", \
            "--server.port=8501", \
            "--server.address=0.0.0.0", \
            "--server.headless=true"]
