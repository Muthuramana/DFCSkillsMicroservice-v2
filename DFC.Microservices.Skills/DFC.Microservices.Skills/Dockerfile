FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY DFC.Microservices.Skills.sln ./
COPY DFC.Microservices.Skills/DFC.Microservices.Skills.csproj DFC.Microservices.Skills/
RUN dotnet restore DFC.Microservices.Skills/DFC.Microservices.Skills.csproj -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/DFC.Microservices.Skills
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DFC.Microservices.Skills.dll"]
