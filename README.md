# ACESSANDO UMA DISTRIBUIÇÃO DO WSL 2 NA REDE LOCAL

## PORTPROXY (ENCAMINHAMENTO DE PORTAS)

### LISTAR TODAS AS REGRAS
```cmd
netsh interface portproxy show all
```

### ADICIONAR UMA REGRA

```cmd
netsh interface portproxy add v4tov4 listenport=<sua_porta_para_redirecionar> listenaddress=0.0.0.0 connectport=<sua_porta_para_conectar_no_wsl> connectaddress=(wsl hostname -I)
```

### EXCLUIR UMA REGRA

```cmd
netsh interface portproxy delete v4tov4 listenport=<sua_porta_para_conectar_no_wsl> listenaddress=0.0.0.0
```

* **Dica:** Substitua `<sua_porta_para_conectar_no_wsl>` para o valor correto da sua configuração WSL.

## FIREWALL (REGRA DE ENTRADA PARA PERMITIR CONEXÕES)

### LISTAR TODAS AS REGRAS DO FIREWALL

```cmd
netsh advfirewall firewall show rule name=all
```

### LISTAR UMA REGRA ESPECÍFICA PELO NOME

```cmd
netsh advfirewall firewall show rule name="WSL 8080"
```

### ADICIONAR UMA REGRA

```cmd
netsh advfirewall firewall add rule name="WSL 8080" dir=in action=allow protocol=TCP localport=8080
```

### EXCLUIR UMA REGRA

```cmd
netsh advfirewall firewall delete rule name="WSL 8080"
```
