FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 5175

ENV ASPNETCORE_URLS=http://*:5175

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dotnet6-MT940Api.csproj", "./"]
RUN dotnet restore "dotnet6-MT940Api.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "dotnet6-MT940Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet6-MT940Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet6-MT940Api.dll"]
