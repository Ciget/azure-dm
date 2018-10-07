FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 52533
EXPOSE 44362

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Coffee/Coffee.csproj Coffee/
RUN dotnet restore Coffee/Coffee.csproj
COPY . .
WORKDIR /src/Coffee
RUN dotnet build Coffee.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Coffee.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Coffee.dll"]
