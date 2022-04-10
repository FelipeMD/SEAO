FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["SEAO.API/SEAO.API.csproj", "SEAO.API/"]
RUN dotnet restore "SEAO.API/SEAO.API.csproj"
COPY . .
WORKDIR "/src/SEAO.API"
RUN dotnet build "SEAO.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SEAO.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SEAO.API.dll"]
