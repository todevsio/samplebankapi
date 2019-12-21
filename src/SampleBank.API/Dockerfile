FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["SampleBank.API/SampleBank.API.csproj", "SampleBank.API/"]
RUN dotnet restore "SampleBank.API/SampleBank.API.csproj"
COPY . .
WORKDIR "/src/SampleBank.API"
RUN dotnet build "SampleBank.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SampleBank.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SampleBank.API.dll"]