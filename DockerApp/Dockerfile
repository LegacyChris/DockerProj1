FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["DockerApp/DockerApp.csproj", "DockerApp/"]
RUN dotnet restore "DockerApp/DockerApp.csproj"
COPY . .
WORKDIR "/src/DockerApp"
RUN dotnet build "DockerApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerApp.dll"]