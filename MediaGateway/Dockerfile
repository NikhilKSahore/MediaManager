# Use the official .NET SDK image as a base image
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env

# Set the working directory inside the container
WORKDIR /app

# Copy the .csproj file to the container
COPY *.csproj ./

# Restore dependencies
RUN dotnet restore

# Copy the entire project to the container
COPY . ./

# Build the project
RUN dotnet publish -c Release -o out

# Build the runtime image
FROM docker.io/microsoft/dotnet/aspnet:5.0

WORKDIR /app
COPY --from=build-env /app/out .

# Expose the port the app will run on
EXPOSE 80

# Define the entry point for the application
ENTRYPOINT ["dotnet", "/MediaManager/MediaGateway/bin/Debug/net6.0/MediaGateway.dll"]
