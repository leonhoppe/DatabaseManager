FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DatabaseManager.Backend/DatabaseManager.Backend.csproj", "DatabaseManager.Backend/"]
RUN dotnet restore "DatabaseManager.Backend/DatabaseManager.Backend.csproj"
COPY . .
WORKDIR "/src/DatabaseManager.Backend"
RUN dotnet build "DatabaseManager.Backend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DatabaseManager.Backend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DatabaseManager.Backend.dll"]
