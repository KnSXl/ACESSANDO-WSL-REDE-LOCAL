# ACESSANDO UMA DISTRIBUIÇÃO DO WSL 2 NA REDE LOCAL

**Impotante:** Esses comandos devem ser realizados usando a versão de administrador do PowerShell.

## VERIFICAR IP DO WSL
```cmd
wsl hostname -I
```

Resultado será algo como: 123.45.678.90

## PORTPROXY (ENCAMINHAMENTO DE PORTAS)

### LISTAR TODAS AS REGRAS
```cmd
netsh interface portproxy show all
```

### ADICIONAR UMA REGRA

```cmd
netsh interface portproxy add v4tov4 listenport=<sua_porta_para_redirecionar> listenaddress=0.0.0.0 connectport=<sua_porta_para_conectar_no_wsl> connectaddress=<ip_wsl>
```

### EXCLUIR UMA REGRA

```cmd
netsh interface portproxy delete v4tov4 listenport=<sua_porta_para_conectar_no_wsl> listenaddress=0.0.0.0
```

* **Importante:** Substitua `<sua_porta_para_conectar_no_wsl>` para o valor correto da sua configuração WSL.

## FIREWALL (REGRA DE ENTRADA PARA PERMITIR CONEXÕES)

### LISTAR TODAS AS REGRAS DO FIREWALL

```cmd
netsh advfirewall firewall show rule name=all
```

### LISTAR UMA REGRA ESPECÍFICA PELO NOME

```cmd
netsh advfirewall firewall show rule name="WSL <sua_porta_para_redirecionar>"
```

### ADICIONAR UMA REGRA

```cmd
netsh advfirewall firewall add rule name="WSL <sua_porta_para_redirecionar>" dir=in action=allow protocol=TCP localport=<sua_porta_para_redirecionar>
```

### EXCLUIR UMA REGRA

```cmd
netsh advfirewall firewall delete rule name="WSL <sua_porta_para_redirecionar>"
```

* **Importante:** Substitua `<sua_porta_para_redirecionar>` para o valor definido na adição da regra (Se foi 8080, "<sua_porta_para_redirecionar>" deverá ser 8080) correto da sua configuração WSL.
