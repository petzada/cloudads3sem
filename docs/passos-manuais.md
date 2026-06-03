# Passos Manuais - AWS, GitHub e Entrega

Este arquivo lista as ações que exigem conta, credenciais, console web ou captura de tela.

## 1. Criar a EC2 na AWS

1. Acesse o Console AWS.
2. Abra o serviço **EC2**.
3. Crie uma instância Ubuntu Server.
4. Escolha um tipo econômico, como `t2.micro` ou `t3.micro`, se disponível.
5. Crie ou selecione um par de chaves SSH.
6. No security group, libere:
   - porta `22` para SSH;
   - porta `80` para HTTP.
7. Finalize a criação e copie o IP público da instância.

## 2. Preparar Docker na EC2

Conecte na instância:

```bash
ssh -i sua-chave.pem ubuntu@IP_PUBLICO_DA_EC2
```

Instale Docker:

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker ubuntu
```

Saia e entre novamente na sessão SSH para aplicar o grupo `docker`.

Teste:

```bash
docker --version
docker ps
```

Crie o diretório do projeto:

```bash
sudo mkdir -p /opt/agroverde-onepage
sudo chown ubuntu:ubuntu /opt/agroverde-onepage
```

## 3. Criar o repositório no GitHub

1. Crie um repositório no GitHub.
2. Faça o push da branch `main`.
3. Confirme que os arquivos aparecem no repositório.

Comandos típicos:

```bash
git init
git branch -M main
git add .
git commit -m "Implementa LAB11 AgroVerde"
git remote add origin URL_DO_REPOSITORIO
git push -u origin main
```

## 4. Cadastrar secrets do GitHub Actions

No repositório GitHub:

1. Acesse **Settings**.
2. Acesse **Secrets and variables**.
3. Entre em **Actions**.
4. Cadastre:

| Secret | Valor |
|---|---|
| `EC2_HOST` | IP público ou DNS público da EC2 |
| `EC2_USER` | `ubuntu` |
| `EC2_SSH_KEY` | conteúdo completo da chave privada `.pem` |
| `EC2_PORT` | `22` |

## 5. Executar o pipeline

O deploy roda automaticamente a cada push na branch `main`.

Também é possível executar manualmente:

1. Abra a aba **Actions**.
2. Selecione **Deploy AgroVerde One-Page**.
3. Clique em **Run workflow**.
4. Aguarde a execução ficar verde.

## 6. Validar a página no ar

Acesse no navegador:

```text
http://IP_PUBLICO_DA_EC2
```

Confirme:

- a página AgroVerde carregou;
- o IP público aparece na barra do navegador;
- o rodapé mostra `Servido por web-srv-01`.

Na EC2, se precisar validar o container:

```bash
docker ps
```

## 7. Gerar PDF e vídeo

1. Preencha `docs/relatorio-lab11.md`.
2. Insira os prints das quatro fases.
3. Exporte o relatório em PDF.
4. Grave o vídeo com base em `docs/roteiro-video.md`.
5. Envie o PDF e o vídeo conforme orientação da disciplina.
