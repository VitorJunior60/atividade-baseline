# Solicitação de Mudança: RFC-001

**IC afetado:** Banco de Dados (MySQL)

**Versão atual:** MySQL 8.4

**Versão proposta:** MySQL 9.0

**Motivo da mudança:**
O MySQL 8.4 está apresentando problemas de desempenho em produção, causando lentidão
e, após uma tentativa de correção não autorizada, erros em consultas. A atualização para
a versão 9.0 visa corrigir os problemas de performance de forma planejada e testada.

**Riscos:**
- Incompatibilidade de queries/sintaxe entre versões do MySQL.
- Possível indisponibilidade durante a migração.
- Comportamento inesperado em funcionalidades não testadas previamente.
- Necessidade de rollback caso a nova versão não seja estável.

**Impacto na aplicação:**
A aplicação Node.js/Express depende diretamente do banco de dados. Alterações na versão
do MySQL podem afetar drivers de conexão, queries e comportamento de transações,
exigindo validação completa antes da liberação em produção.

**Ambientes afetados:**
- Ambiente de desenvolvimento (testes iniciais)
- Ambiente de homologação/staging
- Ambiente de produção (aplicação final)

**Testes necessários:**
- Testes de compatibilidade da aplicação com MySQL 9.0
- Testes de regressão das principais funcionalidades do Sistema de Pedidos
- Testes de performance (comparação antes/depois)
- Testes de rollback

**Plano de implementação:**
1. Provisionar ambiente de homologação com MySQL 9.0.
2. Migrar uma cópia do banco `pedidos` para o novo ambiente.
3. Executar bateria de testes funcionais e de performance.
4. Validar resultados com a equipe técnica.
5. Agendar janela de manutenção para atualização em produção.
6. Atualizar produção e monitorar comportamento pós-implantação.

**Plano de rollback:**
Manter backup completo do banco MySQL 8.4 antes da migração. Em caso de falha crítica,
reverter para a versão 8.4 restaurando o backup e redirecionando a aplicação para a
instância anterior, dentro da janela de manutenção definida.

**Responsável:**
Administrador de Banco de Dados / Equipe de Infraestrutura

**Aprovação:**
Aprovado pela equipe técnica responsável, seguindo o fluxo:
Solicitar → Avaliar impacto → Aprovar/Rejeitar → Implementar/Testar → Verificar/Encerrar