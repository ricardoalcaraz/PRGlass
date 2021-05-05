FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["PRGlass/PRGlass.csproj", "PRGlass/"]
RUN dotnet restore "PRGlass/PRGlass.csproj"
COPY . .
WORKDIR "/src/PRGlass"
RUN dotnet build "PRGlass.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PRGlass.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PRGlass.dll"]
