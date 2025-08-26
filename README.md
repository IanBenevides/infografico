graph TD
    subgraph "Cliente (Navegador do Usuário)"
        U[👤<br>Usuário Corporativo] --> FE[⚛️<br>Aplicação Frontend<br>(React.js)]
    end

    subgraph "Servidor (Hospedagem PaaS ou VPS)"
        BE[🚀<br><b>Backend Monolítico</b><br>(Node.js + Express.js)]
        DB[(🗄️<br>Banco de Dados<br>MySQL)]

        BE <--> DB
    end

    FE -- "1. Requisições HTTP via API REST<br>(Ex: /pedidos, /produtos)<br>Envia e recebe dados em JSON" --> BE
    BE -- "2. Respostas HTTP<br>(JSON com dados, sucesso ou erro)" --> FE
    
    subgraph BE_Internals [Internamente no Backend]
        style BE_Internals fill:#f0f8ff,stroke:#ccc,stroke-dasharray: 5 5
        Roteamento["Rotas (Endpoints da API)"]
        Logica["Lógica de Negócio<br>- Controle de Estoque<br>- Gestão de Pedidos<br>- Autenticação<br>- Relatórios"]
        AcessoDB["Camada de Acesso a Dados<br>(ORM: Sequelize ou Prisma)"]

        Roteamento --> Logica
        Logica --> AcessoDB
    end

    AcessoDB -- "3. Comandos SQL" --> DB
    DB -- "4. Retorno dos Dados" --> AcessoDB

    style U fill:#cde4ff
    style FE fill:#d5f5e3
    style BE fill:#fdebd0
    style DB fill:#ebdef0
