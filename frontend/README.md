# Dashboard - Frontend

O frontend do dashboard é construído com [Vite](https://vitejs.dev/), [React](https://react.dev/), [TypeScript](https://www.typescriptlang.org/), [TanStack Query](https://tanstack.com/query), [TanStack Router](https://tanstack.com/router) e [Tailwind CSS](https://tailwindcss.com).

> A documentação considera compatibilidade com **Next.js** e **Zustand** para gestão de estado.

## Requisitos

- [Bun](https://bun.sh/) (recomendado) ou [Node.js](https://nodejs.org/)

## Início rápido

```bash
bun install
bun run dev
```

Depois, abra: <http://localhost:5173/>

Esse servidor é local (fora do Docker). É o fluxo recomendado durante o desenvolvimento.

## Gerar o Cliente

### Automático

- Ative o ambiente virtual do backend.
- No diretório raiz, rode:

```bash
bash ./scripts/generate-client.sh
```

### Manual

- Suba o stack com Docker Compose.
- Baixe o OpenAPI em `http://localhost/api/v1/openapi.json` para `frontend/openapi.json`.
- Rode:

```bash
bun run generate-client
```

Sempre que o backend mudar, gere o cliente novamente.

## Usar API Remota

Defina `VITE_API_URL` em `frontend/.env`:

```env
VITE_API_URL=https://api.seu-dominio.com
```

## Estrutura

- `frontend/src` - Código principal.
- `frontend/src/assets` - Assets estáticos.
- `frontend/src/client` - Cliente OpenAPI gerado.
- `frontend/src/components` - Componentes do dashboard.
- `frontend/src/hooks` - Hooks customizados.
- `frontend/src/routes` - Rotas e páginas.

## Testes End-to-End (Playwright)

Suba o backend com Docker Compose:

```bash
docker compose up -d --wait backend
```

Rode os testes:

```bash
bunx playwright test
```

Modo UI:

```bash
bunx playwright test --ui
```

Para limpar o ambiente:

```bash
docker compose down -v
```

## Testes Unitários

O frontend suporta testes unitários com **Jest** (quando habilitado no projeto).# FastAPI Project - Frontend

The frontend is built with [Vite](https://vitejs.dev/), [React](https://reactjs.org/), [TypeScript](https://www.typescriptlang.org/), [TanStack Query](https://tanstack.com/query), [TanStack Router](https://tanstack.com/router) and [Tailwind CSS](https://tailwindcss.com/).

## Requirements

- [Bun](https://bun.sh/) (recommended) or [Node.js](https://nodejs.org/)

## Quick Start

```bash
bun install
bun run dev
```

* Then open your browser at http://localhost:5173/.

Notice that this live server is not running inside Docker, it's for local development, and that is the recommended workflow. Once you are happy with your frontend, you can build the frontend Docker image and start it, to test it in a production-like environment. But building the image at every change will not be as productive as running the local development server with live reload.

Check the file `package.json` to see other available options.

### Removing the frontend

If you are developing an API-only app and want to remove the frontend, you can do it easily:

* Remove the `./frontend` directory.

* In the `compose.yml` file, remove the whole service / section `frontend`.

* In the `compose.override.yml` file, remove the whole service / section `frontend` and `playwright`.

Done, you have a frontend-less (api-only) app. 🤓

---

If you want, you can also remove the `FRONTEND` environment variables from:

* `.env`
* `./scripts/*.sh`

But it would be only to clean them up, leaving them won't really have any effect either way.

## Generate Client

### Automatically

* Activate the backend virtual environment.
* From the top level project directory, run the script:

```bash
bash ./scripts/generate-client.sh
```

* Commit the changes.

### Manually

* Start the Docker Compose stack.

* Download the OpenAPI JSON file from `http://localhost/api/v1/openapi.json` and copy it to a new file `openapi.json` at the root of the `frontend` directory.

* To generate the frontend client, run:

```bash
bun run generate-client
```

* Commit the changes.

Notice that everytime the backend changes (changing the OpenAPI schema), you should follow these steps again to update the frontend client.

## Using a Remote API

If you want to use a remote API, you can set the environment variable `VITE_API_URL` to the URL of the remote API. For example, you can set it in the `frontend/.env` file:

```env
VITE_API_URL=https://api.my-domain.example.com
```

Then, when you run the frontend, it will use that URL as the base URL for the API.

## Code Structure

The frontend code is structured as follows:

* `frontend/src` - The main frontend code.
* `frontend/src/assets` - Static assets.
* `frontend/src/client` - The generated OpenAPI client.
* `frontend/src/components` -  The different components of the frontend.
* `frontend/src/hooks` - Custom hooks.
* `frontend/src/routes` - The different routes of the frontend which include the pages.

## End-to-End Testing with Playwright

The frontend includes initial end-to-end tests using Playwright. To run the tests, you need to have the Docker Compose stack running. Start the stack with the following command:

```bash
docker compose up -d --wait backend
```

Then, you can run the tests with the following command:

```bash
bunx playwright test
```

You can also run your tests in UI mode to see the browser and interact with it running:

```bash
bunx playwright test --ui
```

To stop and remove the Docker Compose stack and clean the data created in tests, use the following command:

```bash
docker compose down -v
```

To update the tests, navigate to the tests directory and modify the existing test files or add new ones as needed.

For more information on writing and running Playwright tests, refer to the official [Playwright documentation](https://playwright.dev/docs/intro).
