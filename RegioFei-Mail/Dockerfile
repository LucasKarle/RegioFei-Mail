FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["RegioFei-Mail/RegioFei-Mail.csproj", "RegioFei-Mail/"]
RUN dotnet restore "RegioFei-Mail/RegioFei-Mail.csproj"
COPY . .
WORKDIR "/src/RegioFei-Mail"
RUN dotnet build "RegioFei-Mail.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RegioFei-Mail.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RegioFei-Mail.dll"]
