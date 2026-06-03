# AgroVerde Cooperativa - LAB11 Projeto Cloud

Projeto da disciplina DevOps/LAB para publicar uma one-page na AWS com Docker e CI/CD.

## Case

- **Final do RA:** 2
- **Setor:** Agronegócio / Agroindústria
- **Empresa fictícia:** AgroVerde Cooperativa
- **Foco analítico:** governança de dados, interoperabilidade, LGPD e resistência cultural
- **Página principal:** `index.html`

No final do `index.html` existe a constante `INSTANCE_LABEL`. Ela alimenta o rodapé da página com o rótulo da instância servidora:

```js
const INSTANCE_LABEL = "web-srv-01";
```

Na Fase 1, o print deve mostrar a página aberta pelo IP público da EC2 e o rodapé com `Servido por web-srv-01`.

## Arquitetura

Fluxo da solução:

```text
GitHub -> GitHub Actions -> SSH -> EC2 Ubuntu -> Docker -> Nginx -> index.html
```

Serviços e ferramentas:

- **Amazon EC2:** hospeda a aplicação web.
- **GitHub:** mantém o repositório de código.
- **GitHub Actions:** executa a esteira de CI/CD.
- **Docker:** empacota a one-page em uma imagem Nginx.
- **Nginx:** servidor HTTP usado dentro do container.

## Estrutura do repositório

```text
.
├── .github/workflows/deploy.yml
├── docs/
│   ├── checklist-evidencias.md
│   ├── passos-manuais.md
│   ├── relatorio-lab11.md
│   └── roteiro-video.md
├── 11.0_ProjetoCloud_OnePage.md
├── Dockerfile
├── README.md
└── index.html
```

## Execução local

Abrir a página diretamente:

```bash
start index.html
```

Ou executar com Docker:

```bash
docker build -t agroverde-onepage .
docker run -d --name agroverde-web -p 8080:80 agroverde-onepage
```

Depois acesse:

```text
http://localhost:8080
```

Para parar o container local:

```bash
docker rm -f agroverde-web
```

## Deploy na EC2

O workflow `.github/workflows/deploy.yml` roda em push na branch `main` e também pode ser executado manualmente pelo botão **Run workflow**.

O pipeline faz:

1. Valida `index.html`, `Dockerfile` e o rótulo `web-srv-01`.
2. Empacota o projeto.
3. Envia os arquivos para `/opt/agroverde-onepage` na EC2.
4. Constrói a imagem Docker na EC2.
5. Reinicia o container `agroverde-web` na porta `80`.

Secrets necessários no GitHub:

| Secret | Valor esperado |
|---|---|
| `EC2_HOST` | IP público ou DNS público da EC2 |
| `EC2_USER` | Usuário SSH, normalmente `ubuntu` |
| `EC2_SSH_KEY` | Conteúdo da chave privada `.pem` |
| `EC2_PORT` | Porta SSH, normalmente `22` |

## Evidências da entrega

- **Fase 1:** página no ar via IP público da EC2, com rodapé `web-srv-01`.
- **Fase 2:** tela do repositório GitHub com link visível.
- **Fase 3:** tela do GitHub Actions com execução concluída.
- **Fase 4:** `Dockerfile` e trecho do pipeline mostrando uso do Docker.

Use os documentos em `docs/` para preencher relatório, seguir os passos manuais e preparar o vídeo.
