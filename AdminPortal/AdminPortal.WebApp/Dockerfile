#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["AdminPortal/AdminPortal.WebApp/AdminPortal.WebApp.csproj", "AdminPortal/AdminPortal.WebApp/"]
RUN dotnet restore "AdminPortal/AdminPortal.WebApp/AdminPortal.WebApp.csproj"
COPY . .
WORKDIR "/src/AdminPortal/AdminPortal.WebApp"
RUN dotnet build "AdminPortal.WebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AdminPortal.WebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AdminPortal.WebApp.dll"]