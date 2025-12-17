# PHP Code Injection

**Code Injection** é uma forma de ataque que explora vulnerabilidades em aplicações que permitem o envio e a execução de código. Normalmente é encontrada em aplicações web e ocorre por falhas na validação das entradas do usuário.

---

## Code Injection com `include`

Exemplo básico:
<?php include 'exemplo.php'; ?>
css
Copiar código

Esse é um tipo comum de vulnerabilidade, pois permite incluir páginas PHP dentro de outra página.

Exemplo vulnerável:
<?php include $_GET["pagina"]; ?>
yaml
Copiar código

Nesse caso, o PHP irá incluir (e executar) o arquivo indicado pelo usuário dentro da página principal.

Isso permite que um atacante inclua arquivos locais ou remotos, dependendo da configuração do servidor.

---

## Code Injection com `eval`

`eval` é uma função que recebe uma string contendo código PHP e executa esse código no contexto atual.

Exemplo:
<?php $myvar; $x = $_GET['arg']; eval("$myvar = $x;"); ?>
yaml
Copiar código

Se o usuário acessar:
/index.php?arg=1; echo exec("whoami")

yaml
Copiar código

O código fornecido pelo usuário será executado pelo servidor.

Se `eval` for usado com dados vindos do usuário, um atacante pode executar código arbitrário no servidor, caracterizando **RCE (Remote Code Execution)**.

---

## Riscos do uso de `eval` e `include` inseguros

- Execução de comandos do sistema (`exec`, `system`, `shell_exec`)
- Leitura e escrita de arquivos sensíveis
- Exclusão de dados
- Criação de backdoors
- Escalada de privilégios
- Comprometimento total do servidor

---

## Observação

Nunca utilize `eval` ou `include` com dados fornecidos diretamente pelo usuário sem validação rigorosa. O uso incorreto dessas funções é uma das formas mais críticas de vulnerabilidade em PHP.






