# Use the official .NET Core runtime as the base image
FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
WORKDIR /app

# Use the official .NET Core SDK as the build image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

COPY ConsoleApp1.csproj .

RUN dotnet restore "./ConsoleApp1.csproj"

COPY . .

WORKDIR "/src/"

RUN dotnet build "./ConsoleApp1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "./ConsoleApp1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConsoleApp1.dll"]

