# 📡 Radar de Licitações

**Ferramenta com IA que encontra, pontua e analisa licitações públicas abertas no PNCP, para pequenas empresas fornecedoras decidirem em minutos onde vale a pena cotar.**

👉 **Demo ao vivo:** https://vitorferrante10-dotcom.github.io/radar-licitacoes/

---

## O problema

Trabalho com licitações num negócio de família (fornecimento para órgãos públicos). Só em SP há **centenas de dispensas eletrônicas com proposta aberta ao mesmo tempo**. Encontrar as que combinam com o nosso portfólio exige abrir edital por edital no portal, ler o objeto e conferir prazo, valor e se a disputa é exclusiva para ME/EPP. É um trabalho manual e lento, e oportunidades boas passam do prazo sem ninguém ver.

## A solução

Um painel que roda direto no navegador, sem backend nem instalação:

1. **Coleta ao vivo** todas as contratações com proposta aberta na [API pública do PNCP](https://pncp.gov.br/api/consulta/swagger-ui/index.html), por UF e modalidade (dispensa, pregão, concorrência).
2. **Pontua a aderência (0–100)** de cada uma ao negócio: palavras de interesse, palavras de exclusão, se é aquisição de bens, tempo útil até o encerramento e faixa de valor viável para ME/EPP.
3. **Classifica por segmento** (informática, escritório, mobiliário, limpeza, alimentos, saúde…) e mostra KPIs e gráficos: quantas oportunidades aderentes, valor em jogo, quantas encerram em até 5 dias.
4. **Analisa com IA (Claude):** com um clique, busca os **itens do edital** no PNCP e pede ao Claude um parecer estruturado em JSON: resumo, itens-chave, nota de aderência, se há benefício ME/EPP, riscos, recomendação (participar / avaliar / descartar) e próximo passo.
5. **Exporta CSV** para planilha ou CRM.

## Como usar

- Abra a [demo](https://vitorferrante10-dotcom.github.io/radar-licitacoes/), escolha UF, modalidade e prazo, e ajuste as palavras de interesse ao seu portfólio. Clique em **Buscar**.
- Para os pareceres com IA, abra **“Análise com IA”** e cole sua chave da API da Anthropic. A chave fica só no `localStorage` do seu navegador e vai direto para `api.anthropic.com`.
- Sem chave, o botão “Analisar com IA” ainda mostra os itens do edital e sinaliza o benefício ME/EPP.

## Stack e decisões

| Decisão | Por quê |
|---|---|
| HTML + JavaScript puro, 1 arquivo | Deploy grátis no GitHub Pages; qualquer pessoa usa sem instalar nada |
| API pública do PNCP (consulta + itens) | Fonte oficial e nacional; dados ao vivo |
| Claude via Messages API com saída em JSON | Parecer padronizado que dá para comparar e exportar |
| Score por regras + IA sob demanda | Regras filtram centenas de editais de graça; a IA entra só nos que importam (custo baixo) |
| Chart.js | Gráficos leves, sem build |

## Como foi construído

Construído em poucas horas com **IA como par de programação** (Claude): eu defini o problema, as regras de negócio (o que é uma “boa” licitação para uma ME/EPP: prazo, ticket, exclusividade, tipo de objeto) e o formato do parecer; a IA gerou o código, que eu testei com dados reais do PNCP e fui ajustando.

## Próximos passos

- Alerta diário por e-mail/WhatsApp com as novas oportunidades acima de um score (n8n / GitHub Actions)
- Histórico de preços homologados por item, para sugerir o preço da proposta
- Ajuste do score com base nas licitações que de fato vencemos

---

Feito por **Vitor Ferrante dos Santos** · Engenharia Aeroespacial (UFABC) · [LinkedIn](https://www.linkedin.com/in/vitor-ferrante-dos-santos)
*Projeto independente, sem vínculo com o governo. Os dados são do Portal Nacional de Contratações Públicas.*
