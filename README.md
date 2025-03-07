# Projeto SQUID Italo

Para a criação do servidor hospedeiro Squid foram usados os seguintes recursos:

**Sistema Operacional:**
- Debian 12.9.0 (Utilizado para hospedagem)
  (https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)
- Ubuntu 22.04.5 (Utilizado para teste)
  (https://ubuntu.com/download/alternative-downloads)
- Windows 10 (Utilizado para teste)
  (https://www.microsoft.com/pt-br/software-download/windows10)

**Componentes do Sistema:**
- 4GB de RAM
- Processador com 2 núcleos
- 20GB livres para armazenamento 

**Conexão:**
- Placa de Rede em modo Bridge com acesso a internet

---

## Instalação do Squid

**Atualizar o sistema, melhorar o sistema, instalar o squid:**
```bash
sudo apt update
```
```bash
sudo apt upgrade
```
```bash
sudo apt install squid
```

---

## Comandos para monitoramento

**Iniciar o server squid**
```bash
sudo systemctl start squid
```
**Resetar o server squid (Feito para salvar alterações)**
```bash
sudo systemctl restart squid
```
**Verificar o estado do server squid**
```bash
sudo systemctl status squid
```

---

## Configurar o Squid e criar os arquivos
Para abrir o arquivo de configurações do squid, use o comando:
```bash
sudo nano /etc/squid/squid.conf
```
No caso, ainda vamos precisar de mais dois arquivos para a configuração
1. 

---

## Configuração para conectar ao proxy Squid

Para que o server proxy seja executado com sucesso, deve ter uma configurações antes disso nas máquinas que irão conectar.

**Navegador: Mozilla Firefox**
1. Vá até as três linhas no canto superior direito e depois em Configurações
2. Após isso, na aba Geral, role para baixo até achar a opção Configurar conexão...
3. Na tela que irá aparecer, escolha a opção de proxy manual
   - Escreva o ip da máquina hospedeira do squid. Para descobrir o ip, vá até a máquina e digite no terminal:
     ```bash
     ip a | grep inet
     ```
   - E na outra caixa, digite a porta (Por padrão é 3128). Caso não saiba qual a sua
