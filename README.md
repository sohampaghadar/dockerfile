name: Build and Push Docker Image

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: 6.0 # Replace with your .NET version

      - name: Build and Publish .NET App
        run: |
          dotnet publish -c Release -o output

      - name: Build Docker Image
        uses: docker/build-push-action@v4
        with:
          context: .
          file: Dockerfile
          push: false # Change to true if you want to push to a registry
          tags: myapp:latest
