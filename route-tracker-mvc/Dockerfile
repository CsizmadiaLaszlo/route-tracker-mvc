FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["route-tracker-mvc/route-tracker-mvc.csproj", "route-tracker-mvc/"]
RUN dotnet restore "route-tracker-mvc/route-tracker-mvc.csproj"
COPY . .
WORKDIR "/src/route-tracker-mvc"
RUN dotnet build "route-tracker-mvc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "route-tracker-mvc.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "route-tracker-mvc.dll"]
