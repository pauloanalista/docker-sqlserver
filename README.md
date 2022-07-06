# docker-sqlserver
Instalando Sql Server com Docker em uma máquina Windows com WSL 2

### Baixando a imagem do Sql Server
```
docker pull mcr.microsoft.com/mssql/server
````

### Rodando o container
```
docker run -v ~/docker --name sqlserver -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=1q2w3e4r@#$" -p 1433:1433 -d mcr.microsoft.com/mssql/server
```

### Connection String
Se você utilizou as mesmas configurações deste artigo, sua Connection String será igual abaixo. Caso necessário, modifique as informações que alterou na execução dos containers.
```
Server=localhost,1433;Database=nomeDoSeuBanco;User ID=sa;Password=1q2w3e4r@#$
```

### Erros comuns
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider
Nas novas versões da imagem do SQL Server, no Windows, tem ocorrido um problema de SSL. Para resolver este problema, primeiro execute os seguintes comandos:
```
dotnet dev-certs https --clean
dotnet dev-certs https --trust
```
Feito isto, os certificados HTTPS do .NET estarão atualizados e funcionais. Desta forma, adicione os parâmetros Trusted_Connection e TrustServerCertificate na sua Connection String como mostrado abaixo:
```
Server=localhost,1433;Database=nomeDoSeuBanco;User ID=sa;Password=1q2w3e4r@#$;Trusted_Connection=False; TrustServerCertificate=True;
```

### Instale uma IDE
Aconselho instalar as seguintes IDE´s
- SQL Server Management Studio
- Azure Data Studio
- DBeaver

