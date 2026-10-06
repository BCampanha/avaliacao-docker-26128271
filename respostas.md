# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Beatriz Campanha Silva
Matrícula: 26128271
Usuário do GitHub: BCampanha
Usuário do Docker Hub: bcampanhasenai

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?

Eu usei a imagem base nginx:1.27.2-alpine, o tamanho final da imagem do portal foi 79.7MB.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para
   conferir que o `index.html` está lá dentro.

O Nginx procura os arquivos do site na pasta portal/html/.
O comando para conferir que o index.html está lá dentro é
```
docker exec -it teste-portal ls -l /usr/share/nginx/html                                             
```
Esse comando lista todos os itens dentro da pasta /usr/share/nginx/html para a qual o html/ foi copiado, de acordo com o comando COPY do Dockerfile. O comando retornou
```
-rw-r--r--    1 root     root           497 Oct  2  2024 50x.html
-rwxr-xr-x    1 root     root          1209 Oct  6 00:22 estilo.css
-rwxr-xr-x    1 root     root          2020 Oct  6 00:22 index.html
```
para esse container "teste-portal", portanto a verificação foi bem sucedida.

## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

bcampanhasenai/agrovale-portal:1.0-26128271

https://hub.docker.com/repository/docker/bcampanhasenai/agrovale-portal/

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

Para evitar que as credenciais ou traços dela fiquem salvos nos arquivos do computador local.

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | build e run | Aparece a página inicial do nginx, e não a página de "Voltamos em breve"| Build e run não deram erros, mas a página não está aparecendo | Reescrevendo o Dockerfile: Copio a pasta site/ para o nginx/html, e exponho a porta 80 |
| 2 | | | | |
| 3 | | | | |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

A ordem das portas indica qual é a porta da máquina local (a primeira), e qual é a porta exposta do container (a segunda). Em -p 7071:80, 7071 é a porta do computador local, e 80 é a porta exposta do container.

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

Porque os containers estão em uma rede própria, portanto basta o nome do serviço, que é db.

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

Por questões de segurança. A consulta se dá pelo comando 
`docker exec -it avaliacao-docker-26128271-db-1 mariadb -u root -p`; quando executado, o terminal pede a senha root, definida no .env.

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
