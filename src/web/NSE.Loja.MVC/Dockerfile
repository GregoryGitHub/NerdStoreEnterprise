#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/web/NSE.Loja.MVC/NSE.Loja.MVC.csproj", "src/web/NSE.Loja.MVC/"]
RUN dotnet restore "src/web/NSE.Loja.MVC/NSE.Loja.MVC.csproj"
COPY . .
WORKDIR "/src/src/web/NSE.Loja.MVC"
RUN dotnet build "NSE.Loja.MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NSE.Loja.MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NSE.Loja.MVC.dll"]