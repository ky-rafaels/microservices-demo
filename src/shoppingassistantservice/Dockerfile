# Copyright 2024 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# FROM --platform=$BUILDPLATFORM python:3.12.8-slim@sha256:123be5684f39d8476e64f47a5fddf38f5e9d839baff5c023c815ae5bdfae0df7 AS base
FROM --platform=$BUILDPLATFORM cgr.dev/ky-rafaels.example.com/python:3.12-dev@sha256:7c6c36a606ab7c5e1a4ee1f1d023e11a95fa51e5968d3c8b64305bcad5393786 AS base

# get packages
COPY requirements.txt .
RUN pip install -r requirements.txt

# Enable unbuffered logging
ENV PYTHONUNBUFFERED=1

# get packages
WORKDIR /shoppingassistantservice

# Add the application
COPY . .

# set listen port
ENV PORT="8080"
EXPOSE 8080

ENTRYPOINT ["python", "shoppingassistantservice.py"]
