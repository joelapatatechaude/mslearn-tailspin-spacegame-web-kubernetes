FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
#EXPOSE 80
#ENV ASPNETCORE_URLS=http://+:5000
#EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Tailspin.SpaceGame.LeaderboardContainer/Tailspin.SpaceGame.LeaderboardContainer.csproj", "Tailspin.SpaceGame.LeaderboardContainer/"]

RUN dotnet restore "Tailspin.SpaceGame.LeaderboardContainer/Tailspin.SpaceGame.LeaderboardContainer.csproj"
COPY . .
WORKDIR "/src/Tailspin.SpaceGame.LeaderboardContainer"
RUN dotnet build "Tailspin.SpaceGame.LeaderboardContainer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Tailspin.SpaceGame.LeaderboardContainer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:5000
EXPOSE 5000
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Tailspin.SpaceGame.LeaderboardContainer.dll"]
