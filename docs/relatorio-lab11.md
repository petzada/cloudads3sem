# Relatório LAB11 - Projeto Cloud

## Identificação

- **Projeto:** Publicação da one-page AgroVerde na AWS
- **Case:** Case 2 - Agronegócio / Agroindústria
- **Final do RA:** 2
- **Foco:** governança de dados, interoperabilidade, LGPD e resistência cultural

| Integrante | RA |
|---|---|
| Nome do integrante 1 | RA |
| Nome do integrante 2 | RA |

## Resumo da solução

A empresa fictícia AgroVerde Cooperativa possui uma one-page institucional sobre agricultura digital. A página foi publicada em uma instância Amazon EC2 usando Docker. O container utiliza Nginx para servir o arquivo `index.html`. O processo de atualização é automatizado com GitHub Actions, que acessa a EC2 por SSH, envia o projeto, constrói a imagem Docker e reinicia o container.

Arquitetura:

```text
GitHub -> GitHub Actions -> EC2 Ubuntu -> Docker -> Nginx -> One-page AgroVerde
```

## Fase 1 - Infraestrutura base: EC2 + publicação da página

- **Objetivo:** colocar a one-page no ar em uma instância EC2.
- **Serviço usado:** Amazon EC2.
- **Aplicação:** `index.html` servido pelo container Docker `agroverde-web`.
- **URL pública:** `http://IP_PUBLICO_DA_EC2`
- **Rótulo da instância no rodapé:** `web-srv-01`

**Evidência:** inserir print da página aberta no navegador pelo IP público, mostrando o rodapé com `Servido por web-srv-01`.

> Inserir print da Fase 1 aqui.

## Fase 2 - GitHub

- **Objetivo:** manter e visualizar o repositório de código.
- **Repositório:** https://github.com/petzada/cloudads3sem
- **Arquivos principais:** `index.html`, `Dockerfile`, `.github/workflows/deploy.yml`, `README.md` e documentos em `docs/`.

**Evidência:** inserir print da tela do repositório GitHub com o link visível.

> Inserir print da Fase 2 aqui.

## Fase 3 - GitHub Actions

- **Objetivo:** configurar uma pipeline automática de CI/CD.
- **Workflow:** `.github/workflows/deploy.yml`
- **Gatilho:** push na branch `main` ou execução manual.
- **Ações realizadas:** validação dos arquivos, envio para EC2, build Docker e reinício do container.

**Evidência:** inserir print do workflow e do histórico de execução concluída.

> Inserir print da Fase 3 aqui.

## Fase 4 - Docker / IaaS

- **Objetivo:** elaborar um Dockerfile para suportar a implantação do projeto.
- **Imagem base:** `nginx:alpine`
- **Porta exposta:** `80`
- **Container:** `agroverde-web`

Comandos locais usados para teste:

```bash
docker build -t agroverde-onepage .
docker run -d --name agroverde-web -p 8080:80 agroverde-onepage
```

**Evidência:** inserir print do `Dockerfile` e do uso do Docker no pipeline.

> Inserir print da Fase 4 aqui.

## Conclusão

A solução atende ao LAB11 ao publicar a one-page em uma instância EC2, manter o código no GitHub, automatizar o deploy com GitHub Actions e usar Docker como base de empacotamento da aplicação.
