FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src

COPY *.csproj ./
RUN dotnet restore

COPY . .
RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/runtime:7.0

WORKDIR /app

COPY --from=build /app/publish .

RUN useradd -m appuser
USER appuser

ENTRYPOINT ["dotnet", "Worker.dll"]
