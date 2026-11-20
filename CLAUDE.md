# CLAUDE.md — Memória do projeto

> Este arquivo é lido automaticamente pelo Claude em toda conversa sobre este projeto.
> Escrito com base no que foi possível confirmar no código (novembro de 2026).

## O que é o projeto

Site da **Casa de Oração do Senhor Jesus Cristo**, apresentado como "Rádio Oficial"
(título da página: "Casa de Oração do Senhor Jesus Cristo — Rádio Oficial").
Domínio configurado: **casadojesuscristo.com.br** (arquivo `CNAME`).

O site tem duas partes, tudo no mesmo arquivo:

1. **Site público** (para membros e visitantes): início com versículo, lista de
   congregações filtrada por cidade, galeria de fotos, seção "Sobre / Nossa missão",
   links de redes sociais (Instagram, YouTube, Facebook, WhatsApp, TikTok) e rodapé.
2. **Área restrita** (aberta pelos endereços `#admin`, `#pastor` ou `#obreiro` no fim do
   link), com login e painéis diferentes por tipo de usuário:
   - **Admin**: escalas, avisos, obreiros, programação, congregações, informações da
     igreja, visual, usuários, alterar senha e relatórios financeiros de todas as filiais
     (com gráfico).
   - **Pastor**: o mesmo do admin, menos "Usuários"; no financeiro, preenche o
     relatório mensal da sua filial (dízimos, ofertas, despesas, repasse).
   - **Marketing**: redes sociais, cores do site, galeria de fotos, imagem de fundo,
     alterar senha.
   - **Obreiro**: vê avisos e escalas e confirma presença.

## Tecnologias

- Um único arquivo **HTML** (`index.html`, ~2.400 linhas) com CSS e JavaScript puros
  dentro dele. Não há framework, não há etapa de "build", não há `package.json`.
- Fontes do Google Fonts (Cormorant Garamond e Jost).
- Chart.js 4.4.0 (carregado do cdnjs) só para o gráfico financeiro do admin.
- **Todos os dados são salvos no `localStorage` do navegador** (chave `casaoracao_v3`).
  Não existe servidor nem banco de dados.

## Como rodar, testar e publicar

- **Rodar**: abrir o `index.html` no navegador (ou servir a pasta com qualquer servidor
  estático simples).
- **Testar**: não há testes automatizados no repositório.
- **Publicar**: o arquivo `CNAME` indica hospedagem pelo **GitHub Pages** com o domínio
  casadojesuscristo.com.br. Pelo histórico, as atualizações são feitas enviando o
  `index.html` direto pelo site do GitHub ("Add files via upload") no branch `main`.
  (A configuração do Pages em si fica no GitHub e não dá para confirmar pelo código.)

## Organização dos arquivos

```
index.html   → o site inteiro (público + área restrita)
CNAME        → domínio do GitHub Pages
CLAUDE.md    → esta memória
```

Dentro do `index.html`:
- Linhas iniciais: estilos (CSS), com as cores do site em `:root` e os estilos da área
  admin em `#area-admin`.
- `#site-publico`: o HTML do site público.
- `#area-admin`: tela de login, painel admin/pastor/marketing e painel do obreiro.
- `<script>`: funções `db()` / `gravarDb()` (dados padrão e gravação no navegador),
  `rotear()` (troca entre site público e área restrita), `fazerLogin()`, criação dos
  painéis (`criarPainel...`) e, no final, o módulo financeiro (`initFinanceiro`,
  filiais e relatórios), que é "injetado" no painel admin.

## O que parece pronto

- Visual do site público, menu, rolagem suave, versão para celular.
- Login com bloqueio após 5 tentativas erradas (5 minutos) e sessão de 2 horas.
- Painéis de cada tipo de usuário com cadastro/remoção de escalas, avisos,
  programação, congregações, galeria, redes sociais, cores, usuários e filiais.
- Relatórios financeiros mensais por filial, com fechar/reabrir relatório.
- Proteção básica contra código malicioso nos textos (função `sanitizar`).

## O que parece incompleto ou com problema

1. **Os dados não são compartilhados entre pessoas.** Como tudo fica no `localStorage`,
   o que o admin/marketing muda (fotos, congregações, avisos, escalas, financeiro...)
   aparece **só no navegador de quem mudou**. Visitantes, obreiros e pastores em outros
   aparelhos não veem essas mudanças. Para funcionar de verdade é preciso um banco de
   dados/servidor (ex.: um serviço online).
2. **Senhas expostas.** As senhas iniciais de admin, pastor, obreiro, marketing e das
   filiais estão escritas no próprio código, que é público. Qualquer pessoa pode lê-las.
   O login é feito no navegador, então não oferece segurança real. Os dados
   financeiros também ficam sem proteção.
3. **Não existe player de rádio.** Apesar do nome "Rádio Oficial", não há player de
   áudio nem link de transmissão. Há um campo `liveUrl` vazio e uma prévia de botão
   "Ouvir ao vivo" só na tela de cores do marketing.
4. **A programação não aparece no site público.** O admin edita a programação, mas o
   site público não tem o lugar (`pub-programacao`) onde ela seria exibida.
5. **Textos e números de exemplo**: estatísticas na seção "Sobre" (5k+ ouvintes,
   12 programas, 3 anos, 24h), escalas/avisos de exemplo de 2025, filiais de exemplo
   ("Filial Central/Norte/Sul") e links de exemplo nas redes sociais. Rodapé com © 2025.
6. A função `salvarLanc` aparece duas vezes no código (a segunda substitui a primeira).
7. Um trecho no início do script sempre recria o usuário "marketing" com a senha
   padrão a cada visita, desfazendo uma troca de senha desse usuário.

## Como trabalhar com o dono

- O dono **não é programador**. Responder sempre em **português do Brasil**, com
  linguagem simples, sem jargão técnico (ou explicando quando for inevitável).
- **Explicar o plano antes de qualquer mudança grande** e esperar a aprovação.
- **Nunca pedir senhas, chaves secretas ou dados bancários no chat.** Se algo precisar
  de credencial, explicar onde o próprio dono deve configurar.
- Lembrar que o site é publicado direto do branch `main`: mudanças enviadas ali vão
  ao ar.

## Decisões do dono

- **Remodelar todo o projeto** (decidido em novembro de 2026).
- Usar o site **https://121cc.com/** como base/referência para a remodelação
  (inspiração de estrutura e estilo, sem copiar marca, textos ou imagens de lá).
  Ainda não foi analisado: o acesso a esse site foi bloqueado na conversa em que o
  dono pediu. Para analisar, usar uma conversa no ambiente **radio-casa-oracao**,
  que já libera o acesso ao 121cc.com.
- Antes de começar a remodelação, mostrar ao dono um plano simples e esperar a
  aprovação.

## Informações passadas pelo dono

- Instagram da Casa de Oração: https://www.instagram.com/casadeoracaodosenhorjesuscrist
  (ainda não está colocado no site).
