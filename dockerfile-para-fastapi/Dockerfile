#Base Stage
FROM python:3.11-slim AS build-stage
WORKDIR /app
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt
COPY . /app/

#Production Stage
FROM python:3.11-slim AS production-stage
WORKDIR /app
COPY --from=build-stage /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages
COPY --from=build-stage /usr/local/bin /usr/local/bin
COPY . /app/
RUN useradd -m fastapi_user && chown -R fastapi_user /app
USER fastapi_user
EXPOSE 8000
CMD [ "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000" ]