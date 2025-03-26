FROM mcr.microsoft.com/dotnet/sdk:9.0@sha256:3fcf6f1e809c0553f9feb222369f58749af314af6f063f389cbd2f913b4ad556 AS base
WORKDIR /source
COPY WebAPI/WebAPI.csproj ./WebAPI/
RUN dotnet restore WebAPI/WebAPI.csproj

FROM base AS publish
COPY --from=base /source /source
WORKDIR /source
COPY . .
RUN dotnet publish WebAPI/WebAPI.csproj -o /app --no-restore

FROM publish AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT [ "dotnet", "WebAPI.dll" ]