# Projeto de Infraestrutura como Código: Estrutura de Usuários, Diretórios e Permissões

Este projeto implementa o conceito de Infraestrutura como Código, automatizando a criação de uma estrutura básica de diretórios, grupos de usuários e usuários em um sistema Linux. O script configura as permissões de acesso para garantir a segregação de ambientes e a organização de recursos.

## Conteúdo do Projeto

O projeto consiste em um script Bash que realiza as seguintes configurações no sistema operacional:

### 1. Criação de Diretórios

São criados quatro diretórios principais na raiz do sistema (`/`):
* `/publico`: Destinado a arquivos de acesso geral.
* `/adm`: Para uso exclusivo de usuários administradores.
* `/ven`: Para uso exclusivo de usuários da equipe de vendas.
* `/sec`: Para uso exclusivo de usuários da equipe de secretaria.

### 2. Criação de Grupos de Usuários

São definidos três grupos de usuários para organizar as permissões de acesso:
* `GRP_ADM`
* `GRP_VEN`
* `GRP_SEC`

### 3. Criação de Usuários e Associação aos Grupos

Nove usuários são criados e automaticamente associados aos seus respectivos grupos primários:

* **Membros de `GRP_ADM`:** `carlos`, `maria`, `joao`
* **Membros de `GRP_VEN`:** `debora`, `sebastiana`, `roberto`
* **Membros de `GRP_SEC`:** `josefina`, `amanda`, `rogerio`

    **Atenção sobre senhas:**
    As senhas dos usuários são definidas diretamente no script como `Senha123`. Para ambientes de produção ou de maior segurança, é **altamente recomendável** que você:
    * Substitua as senhas de exemplo por senhas fortes e únicas.
    * Considere remover a definição de senha do script e exigir que o administrador defina as senhas manualmente após a execução do script.
    * Explore métodos mais seguros de gerenciamento de senhas (como solicitar interativamente, usar um sistema de segredos ou gerar senhas aleatórias e armazená-las de forma segura).

### 4. Configuração de Permissões

As permissões de acesso aos diretórios são estabelecidas da seguinte forma:

* `/publico`: Permissões `777` (`rwxrwxrwx`), permitindo leitura, escrita e execução para todos os usuários do sistema.
* `/adm`: O proprietário é `root` e o grupo proprietário é `GRP_ADM`. As permissões são `770` (`rwxrwx---`), concedendo leitura, escrita e execução ao proprietário (`root`) e ao grupo `GRP_ADM`. Outros usuários não possuem acesso.
* `/ven`: O proprietário é `root` e o grupo proprietário é `GRP_VEN`. As permissões são `770` (`rwxrwx---`), concedendo leitura, escrita e execução ao proprietário (`root`) e ao grupo `GRP_VEN`. Outros usuários não possuem acesso.
* `/sec`: O proprietário é `root` e o grupo proprietário é `GRP_SEC`. As permissões são `770` (`rwxrwx---`), concedendo leitura, escrita e execução ao proprietário (`root`) e ao grupo `GRP_SEC`. Outros usuários não possuem acesso.

## Como Usar o Script

Para utilizar este script em seu ambiente Linux (idealmente em uma máquina virtual ou ambiente de teste para segurança):

1.  **Baixe o script:** Faça o download do arquivo `nome_do_seu_script.sh` para o seu sistema Linux.
    *(Recomendação: salve o script com um nome claro como `setup_infra_linux.sh` ou `criar_estrutura_dio.sh`)*

2.  **Dê permissão de execução:** Abra um terminal na pasta onde você baixou o script e execute o comando:

    ```bash
    chmod +x nome_do_seu_script.sh
    ```
    *(Substitua `nome_do_seu_script.sh` pelo nome real do arquivo do script baixado.)*

3.  **Execute o script:** Este script requer privilégios de superusuário para criar diretórios, grupos e usuários. Execute-o com `sudo`:

    ```bash
    sudo ./nome_do_seu_script.sh
    ```

## Teste (Verificação Pós-Execução)

Após a execução do script, você pode verificar as configurações aplicadas ao sistema:

* **Verificar Diretórios e Permissões:**
    ```bash
    ls -ld /publico /adm /ven /sec
    ```
* **Verificar Grupos:**
    ```bash
    getent group GRP_ADM
    getent group GRP_VEN
    getent group GRP_SEC
    ```
* **Verificar Usuários e seus Grupos Primários:**
    ```bash
    id carlos
    id maria
    id joao
    id debora
    id sebastiana
    id roberto
    id josefina
    id amanda
    id rogerio
    ```
