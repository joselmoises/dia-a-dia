# LocalFinder

**Uma plataforma para encontrar serviços em Moçambique**

---

## Visão geral

O *LocalFinder* é uma aplicação web que facilita a busca por **serviços** em Moçambique, como farmácias, lojas, oficinas, clínicas, restaurantes e empresas em geral. O foco principal é ajudar pessoas a encontrarem **onde** os serviços são prestados, exibindo endereços, contactos e a localização no mapa. A experiência é simples e aberta: qualquer pessoa pode pesquisar, adicionar novos serviços ou avaliar de forma anónima — sem necessidade de autenticação.

## Principais funcionalidades

* Registro aberto de serviços por qualquer utilizador (sem login).
* Busca fácil por categoria (farmácia, loja, clínica, etc.), cidade/província ou nome.
* Filtros por proximidade usando geolocalização (mostrar serviços mais próximos de quem procura).
* Página de detalhe para cada serviço com endereço, contactos, horário de funcionamento e fotos.
* Avaliações e comentários anónimos dos utilizadores.
* Exibição dos serviços diretamente no mapa para facilitar navegação.
* API pública para consumo de dados por aplicações mobile/terceiras.

## Benefícios

* Ajuda pessoas a **encontrarem rapidamente o serviço mais próximo**.
* Melhora a visibilidade de pequenos negócios locais.
* Permite que utilizadores avaliem serviços e partilhem experiências, mesmo de forma anónima.
* Reduz a dificuldade comum de não saber onde encontrar certos serviços.

## Tecnologias sugeridas (stack)

* Frontend: Angular / React / Vue (progressive web app recomendado)
* Backend: ASP.NET Core / Node.js (Express) / Django
* Banco de dados: PostgreSQL (principal) + Redis (cache)
* Autenticação: Não obrigatória (opcional para funcionalidades avançadas)
* Mapas: Leaflet ou Mapbox (foco em exibir serviços próximos ao utilizador)
* Deploy: Docker, Docker Compose / Kubernetes

## Estrutura do projecto

```
/localfinder
  ├─ backend/         # API (ex: ASP.NET Core)
  ├─ frontend/        # App web (ex: Angular)
  ├─ infra/           # docker-compose, scripts de deploy
  └─ docs/            # documentação adicional
```

## Como começar (desenvolvimento)

**Pré-requisitos**

* Git
* Docker & Docker Compose (recomendado)
* Node.js (para frontend)
* .NET SDK (se usar ASP.NET Core) ou Python (se usar Django)

**Instalação rápida (com Docker)**

1. Clone o repositório:

```bash
git clone https://github.com/joselmoises/dia-a-dia.git
cd dia-a-dia
```

2. Copie o ficheiro de ambiente e ajuste as variáveis:

```bash
cp .env.example .env
# edite .env conforme necessário
```

3. Levante os serviços:

```bash
docker-compose up --build
```

4. Aceda a `http://localhost:3000` (ou porta configurada)

**Execução local sem Docker**

* Backend: rode o projecto pelo CLI do .NET / Node / Django e certifique-se que `DATABASE_URL` está apontada para um PostgreSQL local.
* Frontend: `npm install && npm start` (ou comando equivalente no framework escolhido)

## API (exemplo simplificado)

* `GET /api/services` — lista serviços (suporta query params: `category`, `city`, `q`, `lat`, `lng`, `radius`)
* `GET /api/services/{id}` — detalhes do serviço
* `POST /api/services` — registrar novo serviço (aberto, sem autenticação)
* `POST /api/reviews` — submeter avaliação ou comentário (anónimo por padrão)

> Documente a API com Swagger / OpenAPI para facilitar consumo por terceiros.

## Modelo de dados (resumo)

* Service: `id, name, identifier, category, address, city, province, contacts[], website, photos[], coordinates, createdAt`
* Review: `id, serviceId, rating, comment, createdAt, author(optional)`
* User (opcional): `id, name, email, role, createdAt` (usado apenas para funções avançadas)

> Recomenda-se gerar um `identifier` não sequencial (hash curto) para evitar guessing de IDs.

## Fluxo de utilização

1. **Registro de serviços** — qualquer pessoa pode adicionar informações (nome, categoria, endereço, contacto, horário, localização no mapa).
2. **Busca por serviços** — utilizadores pesquisam pelo tipo de serviço (ex: “farmácia”) e recebem resultados ordenados pela proximidade.
3. **Visualização no mapa** — os resultados são mostrados no mapa, facilitando encontrar o local mais próximo.
4. **Avaliações anónimas** — utilizadores podem avaliar e comentar sem necessidade de login.

## Privacidade & segurança

* Como não há autenticação obrigatória, proteja o sistema contra spam (captcha, rate-limiting).
* Não exponha dados sensíveis (ex: documentos pessoais).
* Use HTTPS em produção.

## Como contribuir

1. Abra uma *issue* descrevendo a sua proposta ou problema.
2. Fork o repositório e crie uma branch: `feature/nome-da-feature`.
3. Faça commits claros e pequenos.
4. Abra um *pull request* para `main` com descrição do que foi alterado.

## Roadmap (ideias futuras)

* Mobile app (iOS / Android)
* Notificações push para serviços próximos
* Integração com apps de navegação (abrir Google Maps / Waze com a rota até ao serviço)
* Sistema opcional de contas para donos de serviços reclamarem o perfil do seu estabelecimento

## Contacto

Se quiser colaborar ou tiver sugestões, abra uma issue no repositório ou contacte `seu-email@exemplo.com`.

## Licença

Escolha a licença apropriada (por exemplo, MIT). Adicione o ficheiro `LICENSE` ao repositório.
