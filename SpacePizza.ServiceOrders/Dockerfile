#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["SpacePizza.ServiceOrders/SpacePizza.ServiceOrders.csproj", "SpacePizza.ServiceOrders/"]
RUN dotnet restore "SpacePizza.ServiceOrders/SpacePizza.ServiceOrders.csproj"
COPY . .
WORKDIR "/src/SpacePizza.ServiceOrders"
RUN dotnet build "SpacePizza.ServiceOrders.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SpacePizza.ServiceOrders.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SpacePizza.ServiceOrders.dll"]