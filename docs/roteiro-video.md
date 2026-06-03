# Roteiro do Vídeo - LAB11 AgroVerde

Use este roteiro como base para uma apresentação curta.

## 1. Identificação

"Olá, somos a dupla formada por [nome 1] e [nome 2]. Nosso projeto é o LAB11 Projeto Cloud. Como o final do RA é 2, implementamos o Case 2, do setor de Agronegócio e Agroindústria."

"A empresa fictícia escolhida é a AgroVerde Cooperativa, uma cooperativa de soja e milho que usa agricultura digital."

## 2. Apresentação da página

"Esta é a one-page da AgroVerde. Ela apresenta a cooperativa, seus indicadores e a jornada de agricultura digital."

"No rodapé aparece o rótulo `web-srv-01`, que identifica a instância que está servindo a aplicação. Esse ponto é importante para a evidência da Fase 1."

## 3. Arquitetura

"A arquitetura usa GitHub para versionamento, GitHub Actions para CI/CD, uma instância EC2 Ubuntu na AWS, Docker para empacotar a aplicação e Nginx para servir o HTML."

"O fluxo é: fazemos push no GitHub, o GitHub Actions conecta na EC2 por SSH, envia os arquivos, constrói a imagem Docker e reinicia o container publicado na porta 80."

## 4. Demonstração do Docker

"O Dockerfile usa a imagem `nginx:alpine`, copia o `index.html` para o diretório padrão do Nginx e expõe a porta 80."

"Localmente, a aplicação pode ser testada com `docker build` e `docker run`. Na EC2, o mesmo processo é executado pela pipeline."

## 5. Demonstração do CI/CD

"Aqui está o workflow do GitHub Actions. Ele é executado quando ocorre push na branch `main` ou manualmente pela aba Actions."

"A execução valida os arquivos, empacota o projeto, envia para a EC2, constrói a imagem Docker e sobe o container `agroverde-web`."

## 6. Evidências finais

"Como evidências, mostramos a página no ar pelo IP público, o repositório GitHub, o histórico do pipeline e o Dockerfile com sua utilização no deploy."

"Com isso, atendemos às quatro fases do LAB11: EC2, GitHub, GitHub Actions e Docker/IaaS."
