#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["WebApplication9/WebApplication9.csproj", "WebApplication9/"]
RUN dotnet restore "WebApplication9/WebApplication9.csproj"
COPY . .
WORKDIR "/src/WebApplication9"
RUN dotnet build "WebApplication9.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication9.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication9.dll"]