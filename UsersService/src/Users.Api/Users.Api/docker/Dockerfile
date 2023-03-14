# Use the official Microsoft .NET 6 SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Set the working directory inside the container
WORKDIR /src

# Copy the project file and restore the dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application source code
COPY . .

# Build and publish the application
RUN dotnet publish -c Release -o /app

# Use the official Microsoft .NET 6 Runtime image for the final image
FROM mcr.microsoft.com/dotnet/aspnet:6.0

# Set the working directory inside the container
WORKDIR /app

# Copy the published application from the build image
COPY --from=build /app .

# Expose the port your application will run on
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "Users.Api.dll"]
