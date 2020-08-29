#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["SispdChatServer/SispdChatServer.csproj", "SispdChatServer/"]
RUN dotnet restore "SispdChatServer/SispdChatServer.csproj"
COPY . .
WORKDIR "/src/SispdChatServer"
RUN dotnet build "SispdChatServer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SispdChatServer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SispdChatServer.dll"]