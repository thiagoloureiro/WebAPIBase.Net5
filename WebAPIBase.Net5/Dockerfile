#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["WebAPIBase.Net5/WebAPIBase.Net5.csproj", "WebAPIBase.Net5/"]
RUN dotnet restore "WebAPIBase.Net5/WebAPIBase.Net5.csproj"
COPY . .
WORKDIR "/src/WebAPIBase.Net5"
RUN dotnet build "WebAPIBase.Net5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAPIBase.Net5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAPIBase.Net5.dll"]