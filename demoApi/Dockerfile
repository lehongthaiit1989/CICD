# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

# Copy solution and restore dependencies
COPY *.sln .
COPY demoApi/*.csproj ./demoApi/
COPY lth.business/*.csproj ./lth.business/
RUN dotnet restore

# Copy everything and build
COPY . .
WORKDIR /src/demoApi
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "demoApi.dll"]
