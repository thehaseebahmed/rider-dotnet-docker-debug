FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DockerDebug101/DockerDebug101.csproj", "DockerDebug101/"]
RUN dotnet restore "DockerDebug101/DockerDebug101.csproj"
COPY . .
WORKDIR "/src/DockerDebug101"
RUN dotnet build "DockerDebug101.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerDebug101.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerDebug101.dll"]
