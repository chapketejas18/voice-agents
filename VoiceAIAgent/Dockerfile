FROM python:3.11-slim

ENV PYTHONUNBUFFERED=1
ENV TZ=Asia/Kolkata

RUN apt-get update && apt-get install -y \
    tzdata \
    ffmpeg \
    libsndfile1 \
    libportaudio2 \
    libgl1 \
    ca-certificates \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN python -m pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

COPY agent.py .
COPY prompts.py .

EXPOSE 8081

CMD ["python", "agent.py", "start"]