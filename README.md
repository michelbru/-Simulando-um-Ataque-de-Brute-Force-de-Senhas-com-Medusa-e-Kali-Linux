**Simulando Ataque de Brute Force com Medusa e Kali Linux**]


**📋 Descrição do Projeto**
Este projeto documenta a prática de testes de segurança em ambiente controlado, utilizando Kali Linux e a ferramenta Medusa para simular ataques de força bruta contra a máquina vulnerável Metasploitable 2.



**🎯 Objetivos**

Compreender ataques de força bruta em diferentes serviços
Praticar técnicas de enumeração e exploração
Documentar processos de auditoria de segurança
Aplicar medidas de mitigação

**🛠️ Ferramentas Utilizadas**

Kali Linux - Sistema operacional para testes de penetração
Metasploitable 2 - Máquina vulnerável para prática
Medusa - Ferramenta de força bruta
Nmap - Scanner de portas e serviços
Enum4linux - Enumeração de compartilhamentos SMB
smbclient - Cliente SMB para teste de acesso

**🔧 Configuração do Ambiente**
Preparação

Configurei duas VMs no VirtualBox (Kali Linux e Metasploitable 2)
Estabeleci conexão de rede entre as máquinas
Testei conectividade com ping 127.0.0.1

**📝 Testes Realizados**
1. Reconhecimento
bash# Varredura de portas e serviços
nmap -sV -p 21,22,80,445,139 127.0.0.1
2. Enumeração SMB
bash# Enumerar usuários e compartilhamentos
enum4linux -a 127.0.0.1 | tee enum4_output.txt
3. Criação de Wordlists
bash# Lista de usuários
echo -e "user\nmsfadmin\nservice" > smb_users.txt

# Lista de senhas
echo -e "password\n123456\nwelcome123\nmsfadmin" > senhas_spray.txt
4. Password Spraying em SMB
bash# Ataque com Medusa
medusa -h 127.0.0.1 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2 -T 50
5. Validação de Acesso
bash# Testar credenciais válidas
smbclient -L //127.0.0.1 -U msfadmin
6. Teste em HTTP
bash# Consultar módulos disponíveis
medusa -M http -q

# Ataque em serviço web
medusa -h 127.0.0.1 -U users.txt -P pass.txt -M http
🎓 Conceitos Aprendidos
Tipos de Ataques

Brute Force - Tentativa sistemática de todas as combinações
Password Spraying - Uso de senhas comuns contra múltiplos usuários
Credential Stuffing - Reutilização de credenciais vazadas

**Serviços Testados**

FTP (porta 21)
SSH (porta 22)
HTTP (porta 80)
SMB (portas 139/445)

**🔒 Medidas de Mitigação**

**Políticas de Senha Forte**

Mínimo de 12 caracteres
Complexidade obrigatória


**Limitação de Tentativas**

Bloqueio temporário após falhas
CAPTCHA em formulários web


**Autenticação Multifator (MFA)**

Camada adicional de segurança


**Monitoramento**

Logs de tentativas de login
Alertas de atividades suspeitas


**Atualização de Sistemas**

Patches de segurança regulares
Desabilitar serviços desnecessários



**⚠️ Aviso Legal**
Este projeto foi realizado em ambiente controlado para fins educacionais. Testes de penetração sem autorização são ilegais. Sempre obtenha permissão antes de realizar qualquer teste de segurança.
📚 Referências

**Kali Linux** - https://www.kali.org/
**Medusa** - http://www.foofus.net/jmk/medusa/medusa.html
**Metasploitable 2** https://sourceforge.net/projects/metasploitable/files/Metasploitable2/
**Nmap** - https://nmap.org/book/

**👨‍💻 Autor** 
Michel Pascoal
Projeto desenvolvido como parte do desafio de Cibersegurança da DIO.

Data: Novembro/2025
Ambiente: VirtualBox com Kali Linux e Metasploitable 2
