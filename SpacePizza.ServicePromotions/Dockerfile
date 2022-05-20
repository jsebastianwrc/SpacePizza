#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["SpacePizza.ServicePromotions/SpacePizza.ServicePromotions.csproj", "SpacePizza.ServicePromotions/"]
RUN dotnet restore "SpacePizza.ServicePromotions/SpacePizza.ServicePromotions.csproj"
COPY . .
WORKDIR "/src/SpacePizza.ServicePromotions"
RUN dotnet build "SpacePizza.ServicePromotions.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SpacePizza.ServicePromotions.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SpacePizza.ServicePromotions.dll"]