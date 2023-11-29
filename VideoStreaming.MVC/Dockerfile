# Use the official ASP.NET 7 base image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

# Build the application
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy only the project file to restore dependencies
RUN wget https://raw.githubusercontent.com/etahamad/ASPNET-VideoStreaming/main/VideoStreaming.MVC/VideoStreaming.MVC.csproj
RUN dotnet restore VideoStreaming.MVC.csproj

# Copy the entire project and build
COPY . .

WORKDIR /src/
RUN dotnet build -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish -c Release -o /app/publish

# Final image with the published application
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VideoStreaming.MVC.dll"]
