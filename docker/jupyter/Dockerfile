FROM python:3.10-slim as base

# Setup env
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONFAULTHANDLER 1

RUN apt update && apt install -y --no-install-recommends gcc g++ python3-dev libpq-dev libxml2 libxslt-dev nodejs npm

FROM base AS python-deps

# Install pipenv and compilation dependencies
RUN pip install pipenv

ENV PIPENV_VENV_IN_PROJECT=1

# Install python dependencies in /.venv
COPY Pipfile .
COPY Pipfile.lock .
RUN pipenv install --dev && pipenv lock --clear

FROM base AS runtime

# Copy virtual env from python-deps stage
COPY --from=python-deps /.venv /.venv
ENV PATH="/.venv/bin:$PATH"

WORKDIR /jupyter

