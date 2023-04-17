FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["omapp/omapp.csproj", "omapp/"]
RUN dotnet restore "omapp/omapp.csproj"
COPY . .
WORKDIR "/src/omapp"
RUN dotnet build "omapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "omapp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "omapp.dll"]
