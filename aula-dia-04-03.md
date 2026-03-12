# QA Manual — Banco do Stark

Este documento registra a atividade prática de QA Manual realizada sobre a aplicação Banco do Stark, desenvolvida em Python e executada no Google Colab.

O objetivo foi analisar o comportamento do sistema, validar regras de negócio e documentar formalmente:

- Casos de Teste
- Bug Report profissional

------------------------------------------------------------

## Objetivo da Atividade

- Transformar a execução prática em Casos de Teste estruturados.
- Registrar pelo menos 1 Bug Report com padrão profissional.

------------------------------------------------------------

## Metodologia Utilizada

1. Execução das células na ordem definida.
2. Observação das saídas exibidas no notebook.
3. Comparação entre regras esperadas e comportamento real do sistema.
4. Documentação formal dos resultados.

------------------------------------------------------------

## Regras Esperadas (Requisitos do Sistema)

O comportamento correto do sistema deveria respeitar as seguintes regras:

- Titular não pode ser vazio ou conter apenas espaços.
- Depósito deve aceitar apenas valores maiores que zero.
- Saque deve aceitar apenas valores maiores que zero e não pode ultrapassar o saldo disponível.
- Transferência deve aceitar apenas valores maiores que zero.
- Transferência não pode ocorrer para a mesma conta.
- Conta destino deve existir.
- O saldo nunca pode ficar negativo.
- O extrato deve registrar corretamente as operações válidas.

------------------------------------------------------------
PARTE 04 — Casos de Teste
------------------------------------------------------------

### Caso de Teste 1

ID: CT-010  

Título/Objetivo: Validar saque com valor zero  

Pré-condição:  
Conta "pepper" criada com saldo positivo.

Passos:

1. Criar conta "pepper"
2. Depositar 500 na conta
3. Executar sacar('pepper', 0)

Resultado esperado:  
O sistema deveria bloquear o saque com valor zero, exibir mensagem de erro e não registrar a operação no extrato.

Resultado obtido:  
O sistema exibiu mensagem de sucesso e registrou o saque com valor 0.

Status: Fail

Evidência:  
OK - Saque realizado: 0

------------------------------------------------------------

### Caso de Teste 2

ID: CT-011  

Título/Objetivo: Validar criação de conta com titular vazio  

Pré-condição:  
Não deve existir conta com nome vazio.

Passos:

1. Executar criar_conta('')
2. Observar mensagem exibida
3. Verificar estrutura interna de contas

Resultado esperado:  
O sistema deveria impedir a criação da conta e exibir mensagem de erro informando titular inválido.

Resultado obtido:  
O sistema criou a conta e exibiu mensagem de sucesso.

Status: Fail

Evidência:  
OK - Conta criada para:

------------------------------------------------------------

### Caso de Teste 3

ID: CT-012  

Título/Objetivo: Validar bloqueio de saque acima do saldo  

Pré-condição:  
Conta "banner" criada com saldo 0.

Passos:

1. Criar conta "banner"
2. Executar sacar('banner', 100)

Resultado esperado:  
O sistema deve exibir mensagem de saldo insuficiente e não alterar o saldo.

Resultado obtido:  
O sistema exibiu erro de saldo insuficiente e manteve o saldo inalterado.

Status: Pass

Evidência:  
ERRO - Saldo insuficiente

------------------------------------------------------------
PARTE 05 — Bug Report
------------------------------------------------------------

Título: Sistema permite criação de conta com titular vazio  

Severidade: Alta  
Prioridade: Alta  

Ambiente:  
Google Colab  
Python 3.x  
Aplicação Banco do Stark  

Descrição:  
O sistema permite a criação de conta informando titular vazio ('').  
Essa ação viola a regra de negócio que determina que o titular não pode ser vazio ou conter apenas espaços.

Passos para reproduzir:

1. Executar criar_conta('')
2. Observar a mensagem exibida
3. Confirmar que a conta foi adicionada ao dicionário interno

Resultado esperado:  
O sistema deveria bloquear a criação da conta e exibir mensagem de erro.

Resultado obtido:  
O sistema exibiu mensagem de sucesso e criou a conta com titular vazio.

Evidência:  
OK - Conta criada para:

Impacto/Risco:

- Permite cadastro inválido no sistema.
- Compromete integridade dos dados.
- Pode gerar inconsistências futuras em operações financeiras.
- Afeta rastreabilidade das contas.

------------------------------------------------------------

## Conclusão

Durante a execução dos testes foram identificadas falhas relacionadas à validação de entrada e regras básicas de negócio.

As principais inconsistências encontradas envolvem:

- Falta de validação de titular
- Falta de validação de valores iguais a zero

A correção dessas falhas é essencial para garantir:

- Integridade do sistema
- Segurança das operações
- Confiabilidade dos dados financeiros
