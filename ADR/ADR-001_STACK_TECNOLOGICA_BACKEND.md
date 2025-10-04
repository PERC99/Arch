# ADR-001: Escolha da Stack Tecnológica para o Backend

### Status: Proposto

#### Data: 2025-10-04

## 1. Contexto
O projeto de gerenciamento de aluguéis necessita de um backend robusto, seguro e de fácil manutenção para servir uma aplicação frontend (Web e futuramente Mobile). As responsabilidades do backend incluem:

- Gerenciamento de autenticação e autorização de usuários (proprietários).

- Operações CRUD (Create, Read, Update, Delete) para imóveis, inquilinos, contratos e pagamentos.

- Lógica de negócio para cálculos de multas, juros e reajustes.

- Geração de documentos (recibos em PDF).

- Envio de notificações por e-mail.

A decisão sobre a stack principal (linguagem, framework e ORM) é crucial, pois impactará a velocidade de desenvolvimento, a escalabilidade, o custo de manutenção e a facilidade de contratação de futuros desenvolvedores.

## 2. Fatores de Decisão (Decision Drivers)
- Velocidade de Desenvolvimento: A stack deve permitir um desenvolvimento rápido para a criação de um MVP (Minimum Viable Product) e iterações ágeis.

- Ecossistema e Bibliotecas: Acesso a um ecossistema maduro com bibliotecas confiáveis para tarefas comuns (autenticação com JWT, ORM, validação de dados, testes, etc.).

- Escalabilidade: A arquitetura deve ser capaz de suportar um aumento no número de usuários e dados sem a necessidade de uma reescrita completa.

- Segurança: O framework deve oferecer, nativamente ou através de bibliotecas, mecanismos sólidos para mitigar vulnerabilidades comuns (SQL Injection, XSS, CSRF).

- Curva de Aprendizagem: A tecnologia deve ser acessível para novos desenvolvedores que venham a se juntar ao projeto no futuro.

- Custo de Infraestrutura: Facilidade de deploy e compatibilidade com provedores de nuvem modernos e soluções de baixo custo (ex: PaaS, Serverless).

## 3. Opções Consideradas
### Opção 1: Node.js + TypeScript com Framework NestJS e ORM Prisma
- Descrição: Utiliza o ecossistema JavaScript/TypeScript, que é extremamente popular para desenvolvimento web. O NestJS oferece uma arquitetura opinativa e modular (inspirada no Angular), e o Prisma é um ORM moderno e type-safe.

#### Prós:

- Excelente para operações I/O-bound (típicas de APIs REST).

- TypeScript adiciona segurança de tipos, melhorando a manutenibilidade.

- O NestJS força uma arquitetura organizada e escalável.

- Vasto ecossistema do NPM.

- Possibilidade de compartilhar código/tipos com o frontend se ele também for em TypeScript.

#### Contras:

- Menos performático para tarefas pesadas de CPU (não é o foco do projeto).

- A curva de aprendizagem do NestJS pode ser um pouco maior que a de frameworks mais simples como o Express.

### Opção 2: Python com Framework Django e ORM Django ORM
- Descrição: Uma solução "baterias inclusas" extremamente robusta e madura. O Django preza pela velocidade de desenvolvimento e possui funcionalidades prontas para uso, como um painel de administração.

#### Prós:

- Desenvolvimento extremamente rápido para CRUDs e painéis administrativos.

- Ecossistema muito maduro e estável.

- ORM poderoso e bem integrado.

- A sintaxe do Python é considerada limpa e de fácil leitura.

#### Contras:

- Pode ser "opinativo demais" para alguns casos de uso.

- Menos flexível que microframeworks como o Flask para arquiteturas não-padrão.

### Opção 3: Java com Framework Spring Boot e ORM Hibernate (JPA)
- Descrição: Uma das stacks mais utilizadas no mundo corporativo para aplicações robustas e de alta performance. O Spring Boot simplifica a configuração de aplicações Spring.

#### Prós:

- Extremamente performático e robusto.

- Fortemente tipado, o que garante segurança em tempo de compilação.

- Ecossistema vasto e com suporte de longa data.

- Excelente para microsserviços e aplicações de grande escala.

#### Contras:

- Mais verboso em comparação com Node.js e Python.

- Curva de aprendizagem mais acentuada.

- O tempo de build e o consumo de memória podem ser maiores.

## 4. Decisão

### Opção escolhida: Opção 1: Node.js + TypeScript com Framework NestJS e ORM Prisma.

### Justificativa:
Esta stack oferece o melhor equilíbrio entre os fatores de decisão para este projeto. A velocidade de desenvolvimento é alta graças à estrutura do NestJS e à simplicidade do Prisma. O uso de TypeScript de ponta a ponta (potencialmente no frontend também) cria um ambiente de desenvolvimento coeso e reduz bugs, aumentando a manutenibilidade a longo prazo.

O ecossistema NPM é o maior do mundo, garantindo bibliotecas para qualquer necessidade futura. A arquitetura do NestJS, baseada em módulos e injeção de dependência, promove um código organizado e naturalmente escalável. Por fim, o deploy em plataformas modernas como Vercel, AWS Lambda ou Google Cloud Run é simples e com custo otimizado.

Embora Python/Django seja uma excelente alternativa para rapidez, a segurança de tipos do TypeScript e a arquitetura moderna do NestJS/Prisma são diferenciais importantes para a longevidade do projeto. Java/Spring, embora muito poderoso, seria excessivamente complexo (over-engineering) para a fase atual e os requisitos do sistema.

## 5. Consequências
### Positivas
- Manutenibilidade a Longo Prazo: O código será fortemente tipado e bem estruturado.

- Produtividade: A estrutura do NestJS e a facilidade de uso do Prisma permitirão que novas funcionalidades sejam adicionadas de forma rápida e segura.

- Performance: A natureza não-bloqueante do Node.js é ideal para a carga de trabalho de uma API que lida primariamente com requisições de rede e banco de dados.

### Negativas (Riscos a Mitigar)
- Curva de Aprendizagem do Framework: A equipe precisará de um tempo para se familiarizar com os conceitos do NestJS (Módulos, Controllers, Services, Injeção de Dependência) se não tiver experiência prévia.

- Gerenciamento de Dependências: O ecossistema NPM é vasto, mas requer atenção para evitar vulnerabilidades e dependências desatualizadas. O uso de ferramentas como npm audit será necessário.