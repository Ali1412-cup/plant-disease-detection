FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --upgrade pip && \
    pip install torch==2.1.0+cpu torchvision==0.16.0+cpu \
    --find-links https://download.pytorch.org/whl/cpu/torch_stable.html && \
    pip install fastapi==0.104.1 uvicorn==0.24.0 timm==0.9.12 \
    Pillow==10.1.0 python-multipart==0.0.6 numpy==1.24.3

COPY . .

EXPOSE 8080

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8080"]
