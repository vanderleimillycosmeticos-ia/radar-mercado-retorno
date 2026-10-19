# Página-ponte do Radar de Mercado

O Mercado Livre exige que o endereço de retorno do OAuth seja **HTTPS** e fixo. O Radar
roda só no computador do usuário (`http://127.0.0.1:8790`), então esta página, publicada no
GitHub Pages, faz a ponte:

1. o Mercado Livre redireciona para `https://vanderleimillycosmeticos-ia.github.io/radar-mercado-retorno/?code=...&state=...`;
2. a página repassa `code` e `state` para `http://127.0.0.1:8790/oauth/retorno`;
3. o Radar valida o `state` e troca o código pelo token usando PKCE (o `code_verifier`
   e o `client_secret` só existem no computador do usuário).

A página não tem segredo nenhum, não carrega scripts externos e não envia o código para
nenhum outro lugar. Sozinho, o código é inútil para terceiros (PKCE + client secret).
