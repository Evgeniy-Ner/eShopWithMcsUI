#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Microservices/Orders/Orders.WebUI/Orders.WebUI.csproj", "Microservices/Orders/Orders.WebUI/"]
RUN dotnet restore "Microservices/Orders/Orders.WebUI/Orders.WebUI.csproj"
COPY . .
WORKDIR "/src/Microservices/Orders/Orders.WebUI"
RUN dotnet build "Orders.WebUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Orders.WebUI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Orders.WebUI.dll"]