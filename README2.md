[README](./README.md)

# Identity Server 4 Personalizado

No ![](./is4e/vs.svg) crie um novo projeto `Aplicativo Web do ASP.NET Core (Model-View-Controller)`:

### Configurar seu novo projeto

|           Campo | Valor   |
| --------------: | :------ |
| Nome do projeto | is4     |
|           Local | E:\\... |

Clique em `Próximo`

### Informações adicionais

|                Campo | Valor                             |
| -------------------: | :-------------------------------- |
|            Estrutura | .NET 6.0 (Suporte de longo Prazo) |
| Tipo de autenticação | Contas Individuais                |

✅ Configurar para HTTPS

🅾️ Habilitar o Docker

✅ Não use instruções de nível superior

### Configurações iniciais

<details>
<summary>📝 is4\Properties\launchSettings.json</summary>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
	<PropertyGroup>
		<TargetFramework>net6.0</TargetFramework>
		<Nullable>enable</Nullable>
		<ImplicitUsings>enable</ImplicitUsings>
		<UserSecretsId>aspnet-is4c-358cda55-6cad-4abe-91fd-79a81458a207</UserSecretsId>
	</PropertyGroup>
	<ItemGroup>
		<PackageReference Include="Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore" Version="6.0.25" />
		<PackageReference Include="Microsoft.AspNetCore.Identity.EntityFrameworkCore" Version="6.0.25" />
		<PackageReference Include="Microsoft.AspNetCore.Identity.UI" Version="6.0.25" />
		<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="6.0.25" />
		<PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="6.0.25" />
	</ItemGroup>
</Project>
```

</details>

<details>
<summary>📝 is4\Properties\launchSettings.json</summary>

```json
{
	"ConnectionStrings": {
		"DefaultConnection": "Data Source=(LocalDb)\\MSSQLLocalDB;Initial Catalog=TestDatabase6;Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False"
	},
	"Logging": {
		"LogLevel": {
			"Default": "Information",
			"Microsoft.AspNetCore": "Warning"
		}
	},
	"AllowedHosts": "*"
}
```

</details>

### Migrations

```sh
dotnet ef migrations list
dotnet ef database update 00000000000000_CreateIdentitySchema
```

# Tools

### Globais

```sh
dotnet tool install --global dotnet-aspnet-codegenerator --version 6.0.16
dotnet tool uninstall -g dotnet-aspnet-codegenerator
```

### Locais

```sh
dotnet new tool-manifest
dotnet tool install --local dotnet-aspnet-codegenerator --version 6.0.16
```

### Criar a base

```sh
dotnet new mvc -n is4b -f net6.0
```

<details>
<summary>📝 is4b\is4b.csproj</summary>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
	<PropertyGroup>
		<TargetFramework>net6.0</TargetFramework>
		<Nullable>enable</Nullable>
		<ImplicitUsings>enable</ImplicitUsings>
	</PropertyGroup>
	<ItemGroup>
		<PackageReference Include="Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore" Version="6.0.25" />
		<PackageReference Include="Microsoft.AspNetCore.Identity.EntityFrameworkCore" Version="6.0.25" />
		<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="6.0.25" />
		<PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="6.0.25">
			<PrivateAssets>all</PrivateAssets>
			<IncludeAssets>runtime; build; native; contentfiles; analyzers</IncludeAssets>
		</PackageReference>
		<PackageReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Design" Version="6.0.16" />
	</ItemGroup>
</Project>
```

</details>

<details>
<summary>📝 is4b\Properties\launchSettings.json</summary>

```json
{
	"profiles": {
		"is4": {
			"commandName": "Project",
			"dotnetRunMessages": true,
			"launchBrowser": true,
			"applicationUrl": "http://localhost:5000;https://localhost:5001",
			"environmentVariables": {
				"ASPNETCORE_ENVIRONMENT": "Development"
			}
		}
	}
}
```

</details>

```sh
dotnet ef DbContext Scaffold "Data Source=(LocalDb)\\MSSQLLocalDB;Initial Catalog=TestDatabase6;Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False" Microsoft.EntityFra
meworkCore.SqlServer -o Models
```

```sh
dotnet ef migrations add InitialCreate
dotnet ef database update
```

# Identity Server 4

```sh
# Vs -> C# -> Web -> ASP .NET Core Web Application
dotnet new web -f netcoreapp3.1 -n is4
dotnet sln add is4
cd is4
```

<details>
<summary>📝 is4\is4.csproj</summary>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
	<PropertyGroup>
		<TargetFramework>net6.0</TargetFramework>
		<Nullable>enable</Nullable>
		<ImplicitUsings>enable</ImplicitUsings>
	</PropertyGroup>
	<ItemGroup>
		<PackageReference Include="Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore" Version="6.0.25" />
		<PackageReference Include="Microsoft.AspNetCore.Identity.EntityFrameworkCore" Version="6.0.25" />
		<PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="6.0.25" />
		<PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="6.0.25">
			<PrivateAssets>all</PrivateAssets>
			<IncludeAssets>runtime; build; native; contentfiles; analyzers</IncludeAssets>
		</PackageReference>
		<PackageReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Design" Version="6.0.16" />
	</ItemGroup>
</Project>
```

</details>

<details>
<summary>📝 is4\Properties\launchSettings.json</summary>

```json
{
	"profiles": {
		"is4": {
			"commandName": "Project",
			"dotnetRunMessages": true,
			"launchBrowser": true,
			"applicationUrl": "http://localhost:5000;https://localhost:5001",
			"environmentVariables": {
				"ASPNETCORE_ENVIRONMENT": "Development"
			}
		}
	}
}
```

</details>

```sh
dotnet aspnet-codegenerator identity -dc AppDbContext
```
