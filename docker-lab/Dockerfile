FROM python:3.11-slim
WORKDIR /app

# These layers will be cached if requirements.txt doesn't change
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# This layer changes when app.py changes
COPY app.py .

EXPOSE 5000
ENV FLASK_APP=app.py
CMD ["python", "app.py"]
