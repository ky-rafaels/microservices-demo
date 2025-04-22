# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM --platform=$BUILDPLATFORM cgr.dev/ky-rafaels.example.com/python:3.12.10-dev@sha256:c1fe87f34522986cd5a6457c334c1395b634f99c84ebd8832b2ae3d4f0dc372f AS base

FROM base AS builder

COPY requirements.txt .

USER root

RUN pip install --prefix="/install" -r requirements.txt

FROM cgr.dev/ky-rafaels.example.com/python:3.12.10@sha256:c1fe87f34522986cd5a6457c334c1395b634f99c84ebd8832b2ae3d4f0dc372f

WORKDIR /loadgen

USER nonroot

COPY --from=builder /install /usr/local

# Add application code.
COPY locustfile.py .

# enable gevent support in debugger
ENV GEVENT_SUPPORT=True

ENTRYPOINT locust --host="http://${FRONTEND_ADDR}" --headless -u "${USERS:-10}" -r "${RATE:-1}" 2>&1
