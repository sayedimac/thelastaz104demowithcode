#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["thelastaz104demowithcode/thelastaz104demowithcode.csproj", "thelastaz104demowithcode/"]
RUN dotnet restore "thelastaz104demowithcode/thelastaz104demowithcode.csproj"
COPY . .
WORKDIR "/src/thelastaz104demowithcode"
RUN dotnet build "thelastaz104demowithcode.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "thelastaz104demowithcode.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "thelastaz104demowithcode.dll"]