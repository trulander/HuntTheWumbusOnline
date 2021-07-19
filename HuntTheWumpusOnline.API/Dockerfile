FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["HuntTheWumpusOnline.API/HuntTheWumpusOnline.API.csproj", "HuntTheWumpusOnline.API/"]
RUN dotnet restore "HuntTheWumpusOnline.API/HuntTheWumpusOnline.API.csproj"
COPY . .
WORKDIR "/src/HuntTheWumpusOnline.API"
RUN dotnet build "HuntTheWumpusOnline.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HuntTheWumpusOnline.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HuntTheWumpusOnline.API.dll"]
