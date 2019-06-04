FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/App/App.csproj", "src/App/"]
RUN dotnet restore "src/App/App.csproj"
COPY . .
WORKDIR "/src/src/App"
RUN dotnet build "App.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "App.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "App.dll"]