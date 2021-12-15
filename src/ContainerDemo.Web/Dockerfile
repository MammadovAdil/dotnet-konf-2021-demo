FROM mcr.microsoft.com/dotnet/sdk:6.0 as build
WORKDIR /src

COPY ["ContainerDemo.Web/*.csproj", "ContainerDemo.Web/"]
COPY ["ContainerDemo.Services/*.csproj", "ContainerDemo.Services/"]
COPY ["ContainerDemo.Contracts/*.csproj", "ContainerDemo.Contracts/"]

RUN dotnet restore "ContainerDemo.Web/ContainerDemo.Web.csproj"

COPY . .

FROM build as publish
RUN dotnet publish "ContainerDemo.Web/ContainerDemo.Web.csproj" -c RELEASE -o /app/publish --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:6.0 as final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ContainerDemo.Web.dll"]
EXPOSE 80