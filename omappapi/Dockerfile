FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["omappapi/omappapi.csproj", "omappapi/"]
RUN dotnet restore "omappapi/omappapi.csproj"
COPY . .
WORKDIR "/src/omappapi"
RUN dotnet build "omappapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "omappapi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "omappapi.dll"]
