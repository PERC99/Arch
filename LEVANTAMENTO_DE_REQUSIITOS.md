[NOME DO PROJETO] - Requisitos do Sistema

### Versão do Documento: 1.0
### Autor: Gabriel Camelo

### Revisões
|   Data	        |   Revisor         |
|   :--             |   :--             |
|11/10/2025	        |   Gabriel Camelo  |

## 1. Introdução
Este documento detalha os requisitos funcionais e não funcionais para o sistema de gerenciamento de aluguéis [NOME DO PROJETO]. O objetivo deste sistema é auxiliar os proprietários de imóveis (pessoas físicas) no gerenciamento de seus imóveis, inquilinos, contratos e pagamentos de forma simples e eficiente.

## 2. Requisitos Funcionais

### 2.1 Autenticação e Acesso
|   ID      |   Nome do Requisito                   |   Descrição   |
|   :--     |   :--                                 |   :--         |
|   RF-001  |   Cadastro de Usuário (Proprietário)  |   O sistema deve permitir que um novo proprietário se cadastre utilizando nome, e-mail e senha.   |
|   RF-002  |   Login de Usuário                    |   O sistema deve permitir que um usuário cadastrado acesse a plataforma utilizando seu e-mail e senha.   |
|   RF-003  |   Recuperação de Senha    |   O sistema deve fornecer uma funcionalidade para que o usuário possa redefinir sua senha através do e-mail cadastrado.   |

### 2.2 Gerenciamento de Imóveis e Inquilinos
|   ID      |   Nome do Requisito                   |   Descrição   |
|   :--     |   :--                                 |   :--         |
|   RF-004  |   Cadastro de Imóvel                  |   O usuário deve poder cadastrar seus imóveis, informando dados como endereço completo, tipo (casa, apartamento), e uma descrição.    |
|   RF-005  |   Listagem de Imóveis                 |   O sistema deve exibir uma lista de todos os imóveis do usuário, indicando quais estão vagos e quais estão alugados. |
|   RF-006  |   Cadastro de Inquilino               |   O usuário deve poder cadastrar inquilinos, armazenando informações essenciais como nome completo, CPF, e-mail e telefone.   |
|   RF-007  |   Edição de Imóvel/Inquilino          |   O sistema deve permitir a edição e exclusão das informações cadastrais de imóveis e inquilinos. |

### 2.3 Gerenciamento de Contratos e Pagamentos
|   ID      |   Nome do Requisito                   |   Descrição   |
|   :--     |   :--                                 |   :--         |
|   RF-008  |   Criação de Contrato de Aluguel      |   O sistema deve permitir a criação de um contrato vinculando um imóvel a um inquilino, com informações de valor do aluguel, dia do vencimento, data de início e fim do contrato. |
|   RF-009  |   Geração de Cobranças Mensais        |   O sistema deve gerar automaticamente uma cobrança mensal para cada contrato ativo, com base no valor e no dia de vencimento definidos.  |
|   RF-010  |   Registro de Pagamento               |   O proprietário deve poder registrar manualmente o recebimento de um aluguel, alterando o status da cobrança para "Pago".    |
|   RF-011  |   Histórico de Pagamentos             |   O sistema deve exibir um histórico completo de todos os pagamentos (pagos e pendentes) para cada contrato.  |
|   RF-012  |   Anexo de Documentos                 |   O usuário deve poder anexar arquivos (ex: cópia do contrato assinado em PDF) a um contrato de aluguel.  |

### 2.4 Notificações e Lembretes
|   ID      |   Nome do Requisito                   |   Descrição   |
|   :--     |   :--                                 |   :--         |
|   RF-013  |   Notificação de Pagamento Vencido    |   O sistema deve exibir um alerta visual no painel principal para o proprietário sobre os aluguéis que estão com pagamento vencido.   |
|   RF-014  |   Alerta de Vencimento de Contrato    |   O sistema deve notificar o proprietário quando um contrato estiver a 30 dias de seu vencimento, permitindo a preparação para renovação ou nova locação. |
|   RF-015  |   Geração de Recibo de Pagamento      |   Após o registro de um pagamento, o sistema deve permitir a geração de um recibo simples em formato PDF, que pode ser enviado ao inquilino.  |

### 2.5 Relatórios
|   ID      |   Nome do Requisito                   |   Descrição   |
|   :--     |   :--                                 |   :--         |
|   RF-016  |   Relatório Financeiro                |   O sistema deve permitir a geração de um relatório de rendimentos por período (mês/ano), exibindo o total recebido de aluguéis.  |
|   RF-017  |   Relatório de Inadimplência          |   O sistema deve gerar um relatório com a lista de todos os inquilinos com pagamentos pendentes em um determinado mês.    |
|   RF-018  |Exportação de Dados                    |   Os relatórios gerados devem ter a opção de serem exportados em formato .CSV ou .PDF.    |

## 3. Requisitos Não Funcionais
|   ID      |   Nome do Requisito       |   Descrição   |
|   :--     |   :--                     |   :--         |
|   RNF-001 |   Usabilidade             |   A interface do sistema deve ser intuitiva e de fácil utilização para usuários com pouco conhecimento técnico.
|   RNF-002 |    Desempenho             |   As páginas e relatórios do sistema devem carregar em no máximo 3 segundos em uma conexão de internet padrão.
|   RNF-003 |   Segurança               |   Toda a comunicação entre o cliente e o servidor deve ser criptografada utilizando o protocolo HTTPS (SSL/TLS).
|   RNF-004 |   Segurança               |   As senhas dos usuários devem ser armazenadas no banco de dados de forma criptografada (hashed).
|   RNF-005 |   Compatibilidade         |   O sistema deve ser responsivo e funcionar corretamente nos principais navegadores web (Chrome, Firefox, Safari) e em dispositivos móveis (smartphones e tablets).   |
|   RNF-006 |   Confiabilidade          |   O sistema deve possuir uma disponibilidade de 99.5% do tempo (uptime).  |
|   RNF-007 |   Confiabilidade          |   Devem ser realizados backups diários e automáticos do banco de dados para prevenir a perda de informações.
|   RNF-008 |   Manutenibilidade        |   O código-fonte deve seguir padrões de projeto e ser devidamente comentado para facilitar futuras manutenções e evoluções do sistema.    |
