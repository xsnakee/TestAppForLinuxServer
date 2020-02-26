FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TestAppForLinuxServer/TestAppForLinuxServer.csproj", "TestAppForLinuxServer/"]
RUN dotnet restore "TestAppForLinuxServer/TestAppForLinuxServer.csproj"
COPY . .
WORKDIR "/src/TestAppForLinuxServer"
RUN dotnet build "TestAppForLinuxServer.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestAppForLinuxServer.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestAppForLinuxServer.dll"]