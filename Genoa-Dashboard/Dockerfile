FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY Genoa-Dashboard/Genoa-Dashboard.csproj Genoa-Dashboard/
RUN dotnet restore Genoa-Dashboard/Genoa-Dashboard.csproj
COPY . .
WORKDIR /src/Genoa-Dashboard
RUN dotnet build Genoa-Dashboard.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Genoa-Dashboard.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Genoa-Dashboard.dll"]
