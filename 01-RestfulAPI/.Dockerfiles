# Use official .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy everything
COPY . .

# Restore dependencies
RUN dotnet restore

# Build the app
RUN dotnet publish -c Release -o /app

# Use a smaller runtime image for production
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app .

# Render will use this port
ENV ASPNETCORE_URLS=http://+:10000
EXPOSE 10000

# Start the app
ENTRYPOINT ["dotnet", "YourProjectName.dll"]

#added comment