#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/StudentOverflow.API/StudentOverflow.API.csproj", "src/StudentOverflow.API/"]
COPY ["src/StudentOverflow.Infrastructure/StudentOverflow.Infrastructure.csproj", "src/StudentOverflow.Infrastructure/"]
COPY ["src/StudentOveflow.Application/StudentOveflow.Application.csproj", "src/StudentOveflow.Application/"]
COPY ["src/StudentOverflow.Domain/StudentOverflow.Domain.csproj", "src/StudentOverflow.Domain/"]
RUN dotnet restore "src/StudentOverflow.API/StudentOverflow.API.csproj"
COPY . .
WORKDIR "/src/src/StudentOverflow.API"
RUN dotnet build "StudentOverflow.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "StudentOverflow.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StudentOverflow.API.dll"]