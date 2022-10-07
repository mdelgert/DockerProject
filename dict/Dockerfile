#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dict/dict.csproj", "dict/"]
RUN dotnet restore "dict/dict.csproj"
COPY . .
WORKDIR "/src/dict"
RUN dotnet build "dict.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dict.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dict.dll"]