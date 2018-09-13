FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 57269
EXPOSE 44384

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY *.sln .
COPY ["HSTestCoreApp/HSTestCoreApp.csproj", "./HSTestCoreApp/"]
RUN dotnet restore "HSTestCoreApp/HSTestCoreApp.csproj"
COPY . .
WORKDIR "/src/HSTestCoreApp"
RUN dotnet build "HSTestCoreApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HSTestCoreApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app ./
ENTRYPOINT ["dotnet", "HSTestCoreApp.dll"]
