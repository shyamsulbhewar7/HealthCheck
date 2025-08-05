# Use the official .NET SDK image to build and publish the app
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Install git
RUN apt-get update && apt-get install -y git && apt-get clean

# Clone the repository
RUN git clone https://github.com/shyamsulbhewar7/HealthCheck.git

# Set the working directory to the cloned repo
WORKDIR /src/HealthCheck

# Restore dependencies
RUN dotnet restore

# Build and publish the app
RUN dotnet publish -c Release -o /app/out

# Use the runtime image to run the app
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build /app/out .

# Command to run the app
ENTRYPOINT ["dotnet", "HealthCheck.dll"]