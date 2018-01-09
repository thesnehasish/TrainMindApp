FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY TrainMindApp/TrainMindApp.csproj TrainMindApp/
RUN dotnet restore
COPY . .
WORKDIR /src/TrainMindApp
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80/tcp
ENTRYPOINT ["dotnet", "TrainMindApp.dll"]
