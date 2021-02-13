#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["src/webapp/QRCodeProject/QRCodeProject.csproj", "src/webapp/QRCodeProject/"]
RUN dotnet restore "src/webapp/QRCodeProject/QRCodeProject.csproj"
COPY . .
WORKDIR "/src/src/webapp/QRCodeProject"
RUN dotnet build "QRCodeProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "QRCodeProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "QRCodeProject.dll"]