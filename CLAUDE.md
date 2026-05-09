# calcularemprestimo.com — Contexto do Projeto

## Regra crítica
**Nunca fazer commit ou push sem autorização explícita do usuário.** Após qualquer atualização, perguntar: "Quer que eu faça o commit (e push)?"

## O que é este projeto
Refatoração do site **calcularemprestimo.com** — calculadora de empréstimo em HTML+CSS+JS puro, hospedado na Vercel. O objetivo é aplicar o mesmo padrão visual e de UX do projeto **calcularrendapassiva.com** (CRP), disponível em `c:\projetos\calcularrendapassiva`.

## Referência: calcularrendapassiva.com (CRP)
Projeto-irmão já concluído em `c:\projetos\calcularrendapassiva`.
- Mesmo owner, mesmo stack (HTML+CSS+JS puro + Vercel)
- Mesmo design system (dark theme, cards, flip card, gráfico Chart.js)
- Mesmo padrão de UX: flip card, resultados, artigos, email capture, doação
- **Sempre que tiver dúvida sobre padrão, CSS ou estrutura, consulte o CRP.**

## Arquivos base já copiados do CRP
| Arquivo | O que é | Ajuste pendente |
|---|---|---|
| `css/style.css` | Design system completo — usar este | Nenhum |
| `js/header-card.js` | Componente de branding (injeta card automaticamente) | Remover lógica bilíngue; adaptar título/subtítulo para CE |
| `js/email.js` | Captura de email bilíngue | Simplificar para só PT (sem `lang`, sem `isEn`) |
| `api/subscribe.js` | Vercel Function para Brevo (listas PT=11, EN=12) | Confirmar ID da lista PT |
| `vercel.json` | Redirect www→bare + cache headers | **BUG:** domínio no redirect ainda aponta para `calcularrendapassiva.com` — corrigir para `calcularemprestimo.com` |
| `robots.txt` | Base | Nenhum |

## Estrutura legada existente
**Atenção: apenas arquivos minificados disponíveis — o código fonte não foi commitado.**
- `index.min.html` — home minificada (referência para entender a estrutura)
- `results.min.html` — resultados minificados
- `script.min.js` — JS minificado
- `style.min.css` — CSS minificado
- `jquery.mask.min.js` — dependência legada (substituir por vanilla JS)
- `termos-de-uso-e-politicas-de-privacidade.html` — termos (migrar para novo template)
- `logo.png`, `novosistema.png` — imagens (verificar uso)
- `package.json` — build de minificação (html-minifier-terser, terser, clean-css)

**Estratégia:** Ler os `.min` para entender a lógica atual, mas reescrever tudo do zero com o padrão do CRP. Não tentar "desminificar".

## O que o site faz — calculadora de empréstimo
Calculadora com campos (deixar um em branco para calcular):
1. **Valor do empréstimo** — quanto quer pegar emprestado
2. **Número de parcelas** — prazo em meses
3. **Taxa de juros mensal (%)** — custo do crédito
4. **Valor da parcela** — prestação mensal

Sistemas de amortização a suportar: **Sistema Price** (parcelas iguais) como principal. SAC (Sistema de Amortização Constante) como opcional/futuro.

## O que o legado já implementa (via script.min.js)
- Flip card animado: formulário → resultados (já existia)
- **Calcular parcela** (PRICE e SAC): implementado e funciona
- **Calcular prazo** (campo em branco): implementado via loop iterativo
- `sessionStorage` para transferir dados entre pages
- Copiar resultados para clipboard
- **Calcular Taxa:** NÃO implementado — retorna zeros silenciosamente
- **Calcular Valor do Empréstimo:** NÃO implementado — idem
- Máscara de campos: usava jQuery Mask — substituir por vanilla JS no novo código
- Moeda nos resultados: usa `$` em vez de `R$` — corrigir no novo código

## Artigos existentes a preservar (manter URLs exatas)
- `artigos/como-calcular-emprestimo.html` (verificar se existe no servidor)
- `artigos/como-quitar-emprestimos-mais-rapido.html` (verificar se existe)

## Novos artigos a criar (pesquisar volume de busca)
Sugestões de temas com potencial de tráfego:
- Tabela Price vs SAC: qual é melhor?
- Como renegociar dívidas
- Taxa de juros ao mês vs ao ano (como converter)
- CET (Custo Efetivo Total): o que é e como calcular
- Como o score de crédito afeta os juros do empréstimo
- Empréstimo consignado vs pessoal: diferenças

## Objetivo da refatoração
- Reescrever do zero com o padrão do CRP
- Flip card animado: formulário → resultados
- Gráfico de amortização (saldo devedor ao longo do tempo)
- Tabela de parcelas (expansível)
- Seções: artigos, email capture (Brevo), doação (Stripe)
- SEO: sitemap, canonical, structured data, GA4, AdSense, Vercel Analytics
- Apenas PT (sem bilíngue por enquanto)

## Stack e regras técnicas
- HTML + CSS + JS puro — zero jQuery, zero Bootstrap, zero minificador no dev
- `sessionStorage` para passar dados entre `index.html` → `results.html`
- Sem `style.min.css` na raiz — usar apenas `css/style.css`
- Novo JS em `js/calculadora.js` (não usar os `.min.js`)

## Códigos de rastreamento
- **GA4:** `G-V1JD0D4KM1` (do projeto legado calcularemprestimo — usar este, não o do CRP)
- **AdSense:** `ca-pub-5865817649832793` (do projeto legado calcularemprestimo — usar este)
- **Vercel Analytics:** `/_vercel/insights/script.js`
- **Brevo lista PT:** a confirmar (CRP usa lista 11 — verificar se CE vai usar a mesma ou uma nova)
- **Stripe doação:** a confirmar com o usuário

## Deploy
- Site está em produção como HTML/CSS/JS — swap de domínio pode ser feito logo após testes
- Vercel (projeto novo ou existente — verificar com o usuário)
- Testar URL provisória Vercel antes do swap
