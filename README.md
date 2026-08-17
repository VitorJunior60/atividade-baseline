# Atividade Baseline

## Importância da Baseline

Uma baseline é de grande importância para sabermos quais configurações foram usadas em um sistema, servindo como ponto de 
referência confiável que mantém os ambientes parecidos entre si e reduz incompatibilidades de versões, guardando itens de 
configuração e registros de alterações e aprovações. Garante mais segurança em casos de problemas, permitindo que a equipe 
identifique facilmente o último estado estável e retorne a ele, além de sustentar uma automação estável, já que se se sabe 
exatamente qual é o estado esperado. Já quando alterações são feitas sem controle de configuração, o ambiente passa a 
se separar do que está documentado, o que dificulta a identificação de erros.

## Desafio 2 – Mudança não autorizada

### Incidente
*"Um administrador percebeu que o banco MySQL 8.4 estava apresentando problemas de
desempenho e decidiu atualizar diretamente o servidor de produção para MySQL 9.0. A
aplicação continuou utilizando as mesmas configurações e o código não foi alterado. Após a
atualização, algumas consultas começaram a apresentar erros."*

### 1. A baseline foi alterada? Por quê?

Sim, a configuração real do ambiente deixou de corresponder à pré-definida na baseline v1.0, que especificava o MySQL 8.4 e foi alterada para o MySQL 9.0. Isso fez com que o estado do ambiente ficasse diferente do estado oficial aprovado.

### 2. Qual Item de Configuração (IC) foi modificado?

Foi o banco de dados MySQL, que passou da versão 8.4 para a versão 9.0.

### 3. Essa alteração deveria ter sido realizada diretamente em produção?

Não, pois modificou um IC que fazia parte da baseline aprovada sem análise precisa.

### 4. Qual processo deveria ter sido executado antes da alteração?

Deveria ter sido realizada uma RFC (solicitação formal de mudança), seguida pela avaliação do impacto, aprovação ou rejeição, implementação, testes e verificação da alteração.

Fluxo: Solicitar → Avaliar impacto → Aprovar/Rejeitar → Implementar/Testar → Verificar/Encerrar.

### 5. O que deve acontecer com a baseline após uma mudança aprovada?

Deve ser criada uma nova baseline representando o novo estado oficial e aprovado do sistema. A baseline v1.0 cede o lugar à baseline v1.1, que tem o MySQL 9.0.
