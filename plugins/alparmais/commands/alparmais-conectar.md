---
description: Conecta o Claude Code à sua conta do Alpar+ e testa a conexão
---

Ajude a pessoa a conectar o Claude Code ao Alpar+ e confirme que funcionou.

1. Tente chamar a ferramenta `resumo_do_sistema` do servidor `alparmais` (ferramenta `mcp__plugin_alparmais_alparmais__resumo_do_sistema`). É a mais simples, não recebe parâmetros e não altera nada.
2. Se a chamada funcionar, a conta já está conectada. Responda em português, em poucas linhas: confirme a conexão, diga em uma frase o que o resumo mostra (quais módulos existem) e sugira dois exemplos de pergunta, como "Resuma a empresa A0123" ou "Como funciona a baixa de uma obrigação?". Cite a fonte "Alpar+".
3. Se a ferramenta não existir, pedir autenticação ou der erro de acesso, explique o passo a passo:
   - Rode `/mcp` e escolha o servidor `alparmais` (aparece como `plugin:alparmais:alparmais`).
   - Escolha a opção de autenticar. O Claude Code abre o navegador na página de login do Alpar+.
   - Entre com o seu e-mail de trabalho. O Alpar+ descobre sozinho a instância do seu escritório pelo e-mail.
   - Autorize o acesso e volte ao terminal. Depois rode `/alparmais:alparmais-conectar` de novo para testar.
   - Se instalou sem o plugin, o comando manual equivalente é: `claude mcp add --transport http alparmais https://alparmais.alparcontabilidade.com.br/mcp`.
4. Regras: nunca peça nem aceite senha, token ou código no chat. O login acontece só no navegador. Se a pessoa não tiver acesso ao Alpar+, oriente a falar com quem administra o sistema no escritório dela.
5. Se o login funcionar mas as consultas vierem negadas, explique que o Claude só enxerga o que a pessoa vê no Alpar+, e que a permissão se ajusta dentro do próprio sistema.
