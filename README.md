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
No caso, ainda vamos precisar de mais dois arquivos para a configuração, que estão anexados nesse repositorio 
- Agora abra o `squid.conf` e procure a linha `include /etc/squid/conf.d/*.conf` (Você pode usar o comando Ctrl + W e escrever para pesquisar). Você vai digitar os comandos abaixo desta linha.
**Comandos para escrever:**
```bash
acl horario_bloqueado time "/etc/squid/horario_bloqueado.txt"
acl sites_bloqueados dstdomain "/etc/squid/sites_bloqueados.txt"

http_access deny horario_bloqueado
http_access deny sites_bloqueados
```
Logo abaixo vai ter uma linha chamada `http_access deny all`, altere ela para `http_access allow all`.
- Ao final da edição, o arquivo deve estar assim:
- ![image](https://github.com/user-attachments/assets/bd01795d-bf3a-4daa-b30c-875ca085dc59)

**Atenção**
Você pode baixar os arquivos no repositorios ou criar manualmente usando os seguinte comandos:
- Para horários:
```bash
sudo nano /etc/squid/horario_bloqueado.txt
```
- Para sites:
```bash
sudo nano /etc/squid/sites_bloqueados.txt
```
Sempre que criar um arquivo com `nano` você vai direto para a edição de texto. E após a criação basta dar o mesmo comando `nano` descrito para modificar o arquivo. 
- Lembrando que: Para sair do arquivo e salvar as alterações, dê `Ctrl` + `W`, `Y` e `Enter`.


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
   - E na outra caixa, digite a porta (Por padrão é 3128). Caso não saiba qual a sua porta, entre no arquivo `squid.conf`, dê um `Ctrl` + `W` e digite `http_port 3128`.
4. Marque a opção "Usar este proxy também em HTTPS"
5. Clique em `OK`

**Navegador: Google Chrome e Opera**
Estes dois navegadores não são configurados diretamente neles, como no Firefox, você tem que alterar o proxy da máquina. Eis o passo a passo para configurar em Linux e Windows:
#### Linux Ubuntu/Debian:
1. Clique no botão Atividades no canto superior esquerdo e pesquise Configurações
2. Vá em Rede e Proxy de Rede
3. Após clicar na engrenagem, escolha a opção Manual
   - No quadrado maior você digita o ip, e no menor você digita a porta. Faça isso em HTTP e HTTPS
4. Pode apenas fechar e pronto, está configurado

#### Windows:
1. Clique no botão de iniciar do Windows e pesquise Configurações
2. Vá em Rede e Internet e logo após em Proxy
3. A ultima opção é Configurar de proxy manual
   - Digite o ip no quadrado maior e digite a porta no quadrado menor
4. Aperte em Salvar e pronto, está configurado
