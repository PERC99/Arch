# ADR-002: Escolha do Banco de Dados

### Status: Aprovado

#### Data: 2025-10-10

## 1. Contexto
Seguindo a definição arquitetural do projeto, é necessário selecionar o banco de dados que servirá como a camada de persistência principal. O banco de dados irá armazenar informações críticas e altamente relacionais, como:

- Dados de usuários (proprietários e inquilinos).

- Detalhes de imóveis.

- Contratos de aluguel com suas cláusulas e datas.

- Registros financeiros de pagamentos, multas e despesas.

## 2. Fatores de Decisão (Decision Drivers)

- **Integridade e Confiabilidade dos Dados:** Sendo um sistema que lida com contratos e finanças, o suporte a transações ACID (Atomicidade, Consistência, Isolamento, Durabilidade) é mandatório e não negociável.

- **Escalabilidade:** A solução deve ser capaz de crescer em volume de dados e número de requisições concorrentes sem degradação de performance.

- **Flexibilidade do Schema:** Embora os dados sejam primariamente relacionais, a capacidade de armazenar dados semi-estruturados (ex: lista de características de um imóvel, tags) de forma eficiente é um diferencial.

- **Ecossistema e Ferramentas:** Disponibilidade de ferramentas de administração, monitoramento, backup e uma comunidade ativa para suporte.

- **Custo de Hospedagem:** Facilidade de deploy em provedores de nuvem populares (AWS, Google Cloud, Azure) com opções de serviços gerenciados e de baixo custo.

## 3. Opções Consideradas

### Opção 1: PostgreSQL

- Descrição: Um sistema de banco de dados objeto-relacional de código aberto extremamente robusto, conhecido por sua conformidade com os padrões SQL e seu rico conjunto de funcionalidades.

#### Prós:

- **Confiabilidade Superior:** Considerado o padrão ouro em integridade de dados e implementação de transações ACID.

- **Recursos Avançados:** Suporte nativo a tipos de dados avançados como JSONB (JSON indexável e eficiente), Array e extensões poderosas como o PostGIS para dados geoespaciais.

- **Extensibilidade:** Permite a criação de funções customizadas, tipos de dados e operadores, oferecendo grande poder de personalização.

#### Contras:

- Pode ter uma percepção de ser ligeiramente mais complexo para configurar inicialmente por iniciantes em comparação com o MySQL.

### Opção 2: MySQL

- **Descrição:** O banco de dados relacional de código aberto mais popular do mundo, amplamente utilizado em aplicações web.

#### Prós:

- **Popularidade e Facilidade de Uso:** Vasta documentação, comunidade enorme e grande disponibilidade em serviços de hospedagem, incluindo os mais baratos.

- **Performance Comprovada:** Rápido e eficiente para cargas de trabalho web tradicionais (CRUD).

#### Contras:

- Historicamente menos robusto que o PostgreSQL em funcionalidades avançadas e na aplicação estrita de padrões SQL.

- O suporte a JSON é funcional, mas o tipo JSONB do PostgreSQL é geralmente considerado mais poderoso para indexação e consultas.

### Opção 3: MongoDB

- **Descrição:** Um banco de dados NoSQL orientado a documentos, que armazena dados em estruturas semelhantes a JSON.

#### Prós:

- **Esquema Flexível:** Ideal para dados não estruturados ou que mudam com frequência.

- **Escalabilidade Horizontal:** Projetado para escalar facilmente em múltiplos servidores.

#### Contras:

- **Modelo de Dados Inadequado:** A natureza dos dados do projeto (contratos, pagamentos, inquilinos) é inerentemente relacional. Modelar essas relações em um banco NoSQL é mais complexo, pode levar a inconsistências e exige mais lógica na camada de aplicação.

- **Transações Complexas:** Garantir a atomicidade em operações que envolvem múltiplas coleções (tabelas) é significativamente mais desafiador do que em um banco de dados relacional. Este é um risco inaceitável para dados financeiros.

## 4. Decisão

### Opção escolhida: Opção 1: PostgreSQL.

### Justificativa:
O PostgreSQL se alinha perfeitamente com todos os fatores de decisão críticos para o projeto. Sua confiabilidade e integridade de dados são incomparáveis, o que é fundamental para um sistema de gestão financeira e contratual.

A combinação da segurança de tipos do TypeScript/Prisma na aplicação com a rigidez e confiabilidade transacional do PostgreSQL na camada de persistência cria uma arquitetura extremamente robusta e segura.

Além disso, a flexibilidade oferecida por tipos como o JSONB permite que o sistema evolua no futuro, acomodando campos semi-estruturados (como "amenidades do imóvel") sem comprometer a estrutura relacional principal. Essa capacidade de unir o melhor dos mundos relacional e não-relacional no mesmo banco de dados torna o PostgreSQL a escolha técnica superior e mais preparada para o futuro.

Enquanto o MySQL é uma opção viável, o PostgreSQL oferece uma vantagem clara em robustez e funcionalidades avançadas com um custo de aprendizado marginal. O MongoDB é inadequado devido à natureza relacional intrínseca dos dados do domínio.

## 5. Consequências

### Positivas:

- **Máxima Segurança e Integridade dos Dados:** Reduz o risco de inconsistências em registros financeiros e contratuais.

- **Arquitetura "À Prova de Futuro":** O sistema estará preparado para implementar funcionalidades mais complexas sem a necessidade de migrar de banco de dados.

### Negativas (Riscos a Mitigar):

- **Gerenciamento da Infraestrutura:** Um banco de dados como o PostgreSQL exige administração (backups, atualizações, monitoramento).

- **Mitigação do Risco:** A complexidade de gerenciamento será mitigada através da utilização de um serviço de banco de dados gerenciado (Managed Database), como o AWS RDS, Google Cloud SQL, ou Supabase. Essas plataformas automatizam as tarefas operacionais, permitindo que a equipe de desenvolvimento foque exclusivamente na lógica da aplicação, combinando a potência do PostgreSQL com a simplicidade de uma solução PaaS.


