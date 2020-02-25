#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Microservices/Cashbox/Cashbox.WebUI/Cashbox.WebUI.csproj", "Microservices/Cashbox/Cashbox.WebUI/"]
RUN dotnet restore "Microservices/Cashbox/Cashbox.WebUI/Cashbox.WebUI.csproj"
COPY . .
WORKDIR "/src/Microservices/Cashbox/Cashbox.WebUI"
RUN dotnet build "Cashbox.WebUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Cashbox.WebUI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Cashbox.WebUI.dll"]