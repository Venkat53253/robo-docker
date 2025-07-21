# -------------------
# Stage 1: Build
# -------------------
FROM python:3.9.23-alpine3.22 AS builder

WORKDIR /build

# Install build dependencies
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev

COPY requirements.txt .
RUN pip3 install --no-cache-dir --prefix=/install -r requirements.txt


# -------------------
# Stage 2: Final image
# -------------------
FROM python:3.9.23-alpine3.22

EXPOSE 8080
WORKDIR /opt/server

# Runtime dependencies only
RUN apk add --no-cache pcre

# Create app user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
USER roboshop

# Copy installed Python packages from builder
COPY --from=builder /install /usr/local

# Copy application code
COPY --chown=roboshop:roboshop payment.ini .
COPY --chown=roboshop:roboshop *.py .

CMD ["uwsgi", "--ini", "payment.ini"]


# ===========================
# Stage 1: Build dependencies
# ===========================
# FROM python:3.9-slim AS builder

# WORKDIR /opt/build

# # Install build tools and headers required for uwsgi compilation
# RUN apt-get update && apt-get install -y --no-install-recommends \
#     build-essential python3-dev gcc libpcre3-dev \
#     && rm -rf /var/lib/apt/lists/*

# COPY requirements.txt .
# RUN pip3 install --upgrade pip \
#     && pip3 install --no-cache-dir --prefix=/install -r requirements.txt

# # ===========================
# # Stage 2: Final lightweight image
# # ===========================
# FROM python:3.9-slim

# EXPOSE 8080
# WORKDIR /opt/server

# # Copy installed packages from builder
# COPY --from=builder /install /usr/local

# # Copy source code
# COPY requirements.txt .
# COPY payment.ini .
# COPY *.py .

# # Create user
# RUN addgroup --system roboshop && adduser --system --ingroup roboshop roboshop \
#     && chown -R roboshop:roboshop /opt/server

# USER roboshop

# CMD ["uwsgi", "--ini", "payment.ini"]


#FROM python:3.9.23-alpine3.22
# FROM python:3.9-slim
# EXPOSE 8080
# WORKDIR /opt/server
# COPY requirements.txt .
# COPY payment.ini .
# COPY *.py .
# RUN addgroup --system roboshop && adduser --system --ingroup roboshop roboshop \
#     && chown -R roboshop:roboshop /opt/server \
#     && pip3 install -r requirements.txt
# USER roboshop
# CMD ["uwsgi", "--ini", "payment.ini"]

#CMD ["sleep", "1000"]
# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY requirements.txt .
# COPY *.py .
# COPY payment.ini .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi", "--ini", "payment.ini"]