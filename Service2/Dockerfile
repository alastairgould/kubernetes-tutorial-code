FROM microsoft/dotnet:2.0-sdk AS build-env
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out --no-restore /p:PublishWithAspNetCoreTargetManifest="false"

# build runtime image
FROM microsoft/dotnet:2.0-runtime AS runtime
WORKDIR /app
COPY --from=build-env /app/out ./
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80
ENTRYPOINT ["dotnet", "Service2.dll"]
