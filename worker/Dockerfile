FROM python:3.6.3
WORKDIR /app
COPY requirements.txt .
RUN pip install --upgrade "pip<22" setuptools wheel
RUN pip install "setuptools-rust<1.5"
RUN pip install -r requirements.txt
COPY app.py .
EXPOSE 5000
CMD ["gunicorn", "-b", "0.0.0.0:5000", "app:app"]
