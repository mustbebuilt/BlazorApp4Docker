FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY BlazorApp4Docker.csproj .
RUN dotnet restore BlazorApp4Docker.csproj
COPY . .
RUN dotnet build BlazorApp4Docker.csproj -c Release -o /app/build

FROM build AS publish
RUN dotnet publish BlazorApp4Docker.csproj -c Release -o /app/publish

FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY nginx.conf /etc/nginx/nginx.conf