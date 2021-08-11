#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Webapi3/Webapi3.csproj", "Webapi3/"]
RUN dotnet restore "Webapi3/Webapi3.csproj"
COPY . .
WORKDIR "/src/Webapi3"
RUN dotnet build "Webapi3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Webapi3.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Webapi3.dll"]