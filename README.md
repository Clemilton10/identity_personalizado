# Identity Personalizado

<style>@import url("./sty.css");</style>

### Criação

```sh
dotnet new mvc --framework net6.0 --auth Individual --name is4
# ou
dotnet new mvc -f net6.0 -au Individual -n is4
```

No <span class="vs"> </span> clique com <span class="bt_right"> </span> em `is4`:

```csharp
   is4
	⤷ adicionar
		⤷ Novo item com scaffold
			✅ Account/Register
			✅ Account/Login
			✅ Account/Logout
```
