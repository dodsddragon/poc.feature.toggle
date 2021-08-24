#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["poc.feature.toggle.API/poc.feature.toggle.API.csproj", "poc.feature.toggle.API/"]
RUN dotnet restore "poc.feature.toggle.API/poc.feature.toggle.API.csproj"
COPY . .
WORKDIR "/src/poc.feature.toggle.API"
RUN dotnet build "poc.feature.toggle.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "poc.feature.toggle.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "poc.feature.toggle.API.dll"]