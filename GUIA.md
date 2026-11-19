# Guia para configurar seu GitHub

## 1. Criar ou localizar o repositório de perfil

O repositório especial precisa ter exatamente o mesmo nome do seu usuário do GitHub. Por exemplo, se o endereço do seu perfil for `github.com/felipe-dev`, o repositório precisa se chamar `felipe-dev`. Ele deve ser público e conter um `README.md` na raiz.

Documentação oficial: https://docs.github.com/pt/account-and-profile/how-tos/profile-customization/managing-your-profile-readme

## 2. Personalizar o README

1. Abra `README.md`.
2. Use `Ctrl + H` para localizar `SEU_USUARIO` e substitua pelo seu nome de usuário exato do GitHub.
3. Confira se o link do LinkedIn está correto.
4. Escolha se deseja divulgar um e-mail. Não publique um endereço pessoal se não quiser recebê-lo publicamente.
5. Na seção de projetos, substitua o comentário de exemplo por dois a quatro projetos reais, com link, objetivo e tecnologias utilizadas.
6. Remova ou mantenha comentada a seção de imagens pessoais até enviar suas próprias imagens.

Os trechos entre `<!--` e `-->` são comentários HTML: não aparecem na página publicada, mas ficam visíveis quando você edita o arquivo.

## 3. Publicar a animação Tron Arcade

O arquivo `.github/workflows/main.yml` utiliza a action [Nicsilver/commit-arcade](https://github.com/marketplace/actions/commit-arcade), configurada para jogar **Tron** sobre seu gráfico de contribuições.

1. O workflow já está no caminho correto: `.github/workflows/main.yml`.
2. Ele gera duas imagens: `dist/tron.svg` (tema neon para modo escuro) e `dist/tron-light.svg` (tema claro).
3. A action `crazy-max/ghaction-github-pages` publica os arquivos gerados na branch `output`.
4. O README já aponta para `output/tron.svg` e `output/tron-light.svg`.
5. Para acompanhar a execução, abra **Actions → Tron Arcade Contribution Graph**. O workflow também pode ser iniciado manualmente com **Run workflow**; além disso, roda diariamente às 03:00 UTC e quando há push na branch `main`.

Se a publicação falhar por permissão, abra **Settings → Actions → General → Workflow permissions**, selecione **Read and write permissions** e salve.

A animação usa suas contribuições reais; ela não cria commits nem aumenta a quantidade de contribuições. A primeira execução precisa terminar com sucesso para que os SVGs apareçam na branch `output`.

## 4. Configurar corretamente o autor dos próximos commits

O nome e o e-mail gravados localmente pelo Git determinam a identidade do autor dos próximos commits. Para configurar todos os repositórios deste computador, abra o terminal e execute:

```bash
# Nome que aparecerá como autor dos próximos commits
git config --global user.name "Felipe Alejandro Oliveira Sousa"

# Use o endereço verificado da sua conta ou o endereço noreply do próprio GitHub.
# Consulte o valor exato em GitHub → Settings → Emails.
git config --global user.email "SEU_EMAIL_VERIFICADO_OU_NOREPLY"

# Confira os valores salvos
git config --global --get user.name
git config --global --get user.email
```

Para configurar apenas um repositório, entre na pasta dele e execute os mesmos comandos sem `--global`.

**Privacidade:** prefira o endereço `noreply` que aparece em GitHub → Settings → Emails caso não queira expor seu e-mail pessoal nos commits.

## 5. Por que commits antigos podem não aparecer no gráfico?

O GitHub só associa os commits à sua conta quando o e-mail usado no commit está vinculado à conta. Além disso, para aparecerem no gráfico, commits precisam cumprir os critérios de branch e repositório do GitHub (por exemplo, branch padrão ou `gh-pages`, repositório que não seja apenas um fork e relação adequada com o repositório).

Se os commits antigos foram feitos com outro e-mail seu:

1. Abra GitHub → **Settings → Emails**.
2. Adicione e confirme o endereço que foi usado nos commits antigos, se possível.
3. Aguarde a atualização do gráfico; o GitHub informa que ela pode levar até 24 horas.

Documentação: https://docs.github.com/en/account-and-profile/how-tos/contribution-settings/troubleshooting-missing-contributions

## 6. Corrigir o último commit, se o autor estiver realmente errado

Faça isso apenas quando o último commit foi feito por você e contém uma identidade incorreta. Na pasta do projeto:

```bash
# Corrige o autor do último commit local, mantendo a mensagem atual
git commit --amend --author="Felipe Alejandro Oliveira Sousa <SEU_EMAIL_VERIFICADO>" --no-edit
```

Se esse commit já foi enviado ao GitHub, reescreverá o histórico remoto. Em uma branch só sua, depois de conferir a alteração, pode ser necessário:

```bash
git push --force-with-lease
```

**Cuidado:** não faça force push em branch compartilhada sem combinar com a equipe. Alterar commits antigos muda seus identificadores e pode atrapalhar quem já baixou o histórico.

Para corrigir somente a mensagem do último commit:

```bash
git commit --amend -m "docs: atualiza README do perfil"
```

## 7. Como escrever mensagens de commit melhores

Use mensagens curtas que descrevam a mudança real:

```text
feat: adiciona validação ao formulário
fix: corrige cálculo do total
docs: atualiza instruções do projeto
refactor: organiza classes de serviço
test: adiciona testes para cadastro
```



## 8. Onde adicionar imagens

A pasta `images/interesses/` foi criada como local sugerido. Envie nela arquivos como `cyberpunk.gif`, `skyrim.jpg` ou `project-zomboid.jpg` e, depois, retire os comentários da seção **Fora do código** no README. Os nomes no Markdown precisam ser idênticos aos arquivos enviados.

Para tecnologias, use os ícones do Skill Icons; não precisa baixar cada logo manualmente. Para imagens de jogos, prefira capturas de tela suas, artes próprias ou imagens com licença/permissão adequada.

## Sites úteis

- GitHub Docs — README do perfil: https://docs.github.com/en/account-and-profile/how-tos/profile-customization/managing-your-profile-readme
- Skill Icons — ícones de linguagens e ferramentas: https://skillicons.dev/
- GitHub Readme Stats — cartões de estatísticas: https://github.com/anuraghazra/github-readme-stats
- Commit Arcade — jogos animados no gráfico de contribuições: https://github.com/marketplace/actions/commit-arcade
- Shields.io — badges personalizados: https://shields.io/
- GitHub Profile Trophy — troféus opcionais: https://github.com/ryo-ma/github-profile-trophy

## Checklist antes de publicar

- [ ] O repositório tem o mesmo nome do meu usuário do GitHub.
- [ ] Substituí `SEU_USUARIO` no README.
- [ ] O link do LinkedIn está correto.
- [ ] Não deixei e-mail ou informação pessoal que não queira divulgar.
- [ ] Os projetos destacados são meus e têm links válidos.
- [ ] As tecnologias listadas são ferramentas que realmente estudei ou utilizei.
- [ ] O workflow Tron Arcade executou sem erros.
