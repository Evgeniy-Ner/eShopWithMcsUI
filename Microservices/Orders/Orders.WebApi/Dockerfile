#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Microservices/Orders/Orders.WebApi/Orders.WebApi.csproj", "Microservices/Orders/Orders.WebApi/"]
RUN dotnet restore "Microservices/Orders/Orders.WebApi/Orders.WebApi.csproj"
COPY . .
WORKDIR "/src/Microservices/Orders/Orders.WebApi"
RUN dotnet build "Orders.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Orders.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Orders.WebApi.dll"]