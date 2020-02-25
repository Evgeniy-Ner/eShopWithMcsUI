#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Microservices/Users/Users.WebUI/Users.WebUI.csproj", "Microservices/Users/Users.WebUI/"]
RUN dotnet restore "Microservices/Users/Users.WebUI/Users.WebUI.csproj"
COPY . .
WORKDIR "/src/Microservices/Users/Users.WebUI"
RUN dotnet build "Users.WebUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Users.WebUI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Users.WebUI.dll"]