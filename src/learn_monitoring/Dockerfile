
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["learn_monitoring.csproj", "./"]
RUN dotnet restore "./learn_monitoring.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "learn_monitoring.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "learn_monitoring.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "learn_monitoring.dll"]