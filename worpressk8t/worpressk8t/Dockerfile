FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["worpressk8t/worpressk8t.csproj", "worpressk8t/"]

RUN dotnet restore "$PROJECT_DIR/worpressk8t.csproj"
COPY . .
WORKDIR "/src/worpressk8t"
RUN dotnet build "worpressk8t.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "worpressk8t.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "worpressk8t.dll"]