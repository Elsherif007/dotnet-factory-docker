#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /src
COPY ["FactoryMethod/FactoryMethod.csproj", "FactoryMethod/"]
RUN dotnet restore "FactoryMethod/FactoryMethod.csproj"
COPY . .
WORKDIR "/src/FactoryMethod"
RUN dotnet build "FactoryMethod.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FactoryMethod.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FactoryMethod.dll"]