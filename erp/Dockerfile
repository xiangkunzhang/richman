FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["erp/erp.csproj", "erp/"]
RUN dotnet restore "erp/erp.csproj"
COPY . .
WORKDIR "/src/erp"
RUN dotnet build "erp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "erp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "erp.dll"]