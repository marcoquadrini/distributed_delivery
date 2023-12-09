FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["pdp/pdp.csproj", "pdp/"]
RUN dotnet restore "pdp/pdp.csproj"
COPY . .
WORKDIR "/src/pdp"
RUN dotnet build "pdp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "pdp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "pdp.dll"]
