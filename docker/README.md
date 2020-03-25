# Lambda Python 3.8 module to access RedShift

# Build
```bash
docker build -t lambda_py38_psycopg2 .
```

# Retrieve the artifact
```bash
docker run --name psycopg2 lambda_py38_psycopg2
docker cp psycopg2:/build/psycopg2.zip ./
docker stop psycopg2
docker rm psycopg2
```