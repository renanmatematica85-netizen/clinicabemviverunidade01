# Lar de Idosos Bem Viver — site institucional

Site de página única, responsivo, sem dependências de build. Basta abrir `index.html`
no navegador ou subir a pasta inteira para qualquer hospedagem.

---

## 1. O que trocar antes de publicar

Abra o `index.html`, role até o final e localize o bloco **`const CONFIG = {`**.
Todos os dados de contato do site saem daí — é o único lugar que você precisa editar.

| Campo | O que colocar |
|---|---|
| `whatsapp` | Só números, com país e DDD: `5551999999999` |
| `telefoneExibicao` | Como o telefone aparece na tela: `(51) 3333-3333` |
| `endereco` | Endereço completo com CEP |
| `email` | E-mail que recebe os contatos do formulário |
| `instagram` | URL completa do perfil. Deixe `""` para esconder o botão |
| `instagramHandle` | Como o @ aparece na tela: `@seuinstagram` |
| `msgWhatsapp` | Texto que já vem digitado quando alguém clica no WhatsApp |
| `horario` / `horarioVisitas` | Horário de funcionamento exibido no site |

Além do `CONFIG`, ainda vale revisar manualmente:

- **Depoimentos** — confira se os textos da seção refletem depoimentos reais e autorizados de familiares.
- **Mapa** — na seção de contato, troque o `src` do `<iframe>` do Google Maps.
  No Google Maps: encontre o local → *Compartilhar* → *Incorporar um mapa* → copie o `src`.
- **Bloco `application/ld+json`** (SEO) — atualize nome, telefone, e-mail, endereço e o domínio.
- **Meta tags no `<head>`** — troque `https://www.larbemviver.com.br/` pelo domínio real
  em `canonical`, `og:url` e `og:image`.

---

## 2. Fazer o formulário chegar no seu e-mail

O formulário usa o **FormSubmit** (gratuito, sem cadastro, sem back-end). Ele monta o
endereço de envio sozinho a partir do `email` que está no `CONFIG` — não precisa editar
mais nada além disso.

1. Confirme que o campo `email` do `CONFIG` está com o e-mail certo.
2. Publique o site.
3. Envie **um** formulário de teste. Você vai receber um e-mail do FormSubmit com um
   link de confirmação — **clique nele**. Isso só acontece uma vez.
4. Pronto: a partir daí todos os envios caem na sua caixa de entrada.

O formulário também exige que o visitante marque a caixa de **consentimento LGPD**
antes de enviar — o botão fica bloqueado até isso ser feito.

---

## 3. Publicar

**Opção mais simples e recomendada (grátis): Vercel**
1. Suba a pasta `bem-viver` inteira (com a subpasta `assets/img` junto) para um
   repositório no GitHub — arraste a pasta inteira pelo GitHub Desktop ou pela tela
   de upload do site, garantindo que a estrutura de pastas não se perca.
2. Em [vercel.com](https://vercel.com), crie um projeto a partir desse repositório.
3. Se o `index.html` não estiver na raiz do repositório (por exemplo, dentro de uma
   pasta chamada `bem-viver`), configure em **Settings → Build and Deployment →
   Root Directory** o nome dessa pasta.
4. O arquivo `vercel.json` já incluso cuida dos cabeçalhos de segurança automaticamente.

**Alternativa igualmente simples:** [Netlify Drop](https://app.netlify.com/drop) — arraste a pasta `bem-viver` inteira, sem precisar de GitHub.

**Hospedagem tradicional (Hostinger, HostGator, Locaweb):**
- Envie o conteúdo da pasta para `public_html/` via FTP ou gerenciador de arquivos,
  mantendo a subpasta `assets/img` junto do `index.html`.

Depois, aponte o domínio e ative o SSL (todas as opções acima oferecem certificado gratuito).

> **O erro mais comum:** publicar só o arquivo `index.html` sozinho, sem a pasta
> `assets/img` ao lado. Sem essa pasta, nenhuma foto do site aparece. Sempre publique
> a pasta `bem-viver` completa.

---

## 4. Estrutura de arquivos

Todos os nomes abaixo são exatamente os mesmos usados no código (`src="assets/img/..."`)
— não renomeie os arquivos, ou as fotos correspondentes somem do site.

```
bem-viver/
├── index.html                          ← site inteiro (HTML + CSS + JS)
├── LEIA-ME.md                          ← este arquivo
├── vercel.json                         ← cabeçalhos de segurança (deploy na Vercel)
└── assets/img/
    ├── logo.png                        (logotipo — favicon e ícone do site)
    ├── fachada-real.jpg                (carrossel do topo — fachada)
    ├── vitrine-logo.jpg                (carrossel do topo — vitrine/entrada)
    ├── convivio-jardim-real.jpg        (seção Sobre nós)
    ├── logo-vidro.jpg                  (seção Sobre nós — logo aplicado em vidro)
    ├── estrutura-quarto.jpg            (seção Nossa Estrutura)
    ├── estrutura-sala1.jpg             (seção Nossa Estrutura)
    ├── estrutura-saida-jardim.jpg      (seção Nossa Estrutura)
    ├── estrutura-tv1.jpg               (seção Nossa Estrutura)
    ├── estrutura-tv2.jpg               (seção Nossa Estrutura)
    ├── estrutura-solario.jpg           (seção Nossa Estrutura)
    ├── estrutura-descanso.jpg          (seção Nossa Estrutura)
    ├── estrutura-patio-refeicoes.jpg   (seção Nossa Estrutura)
    └── porque-01.jpg … porque-17.jpg   (seção "Por que escolher a Bem Viver?", 17 artes)
```

Ao todo são **30 arquivos de imagem**, e cada um deles é referenciado pelo menos uma vez
no `index.html`. Não existe mais nenhum arquivo "sobrando" na pasta — versões antigas
ou de teste que não apareciam no site foram removidas.

Se quiser trocar alguma foto por uma nova, o jeito mais simples é substituir o arquivo
mantendo exatamente o mesmo nome (mesma grafia, minúsculas, mesma extensão `.jpg`).
Isso importa principalmente ao publicar na Vercel/GitHub: ao contrário do Windows, o
servidor diferencia maiúsculas de minúsculas no nome do arquivo.

---

## 5. Recursos já implementados

- Layout responsivo (desktop, tablet e celular)
- Botão flutuante de WhatsApp com efeito de pulso
- Carrossel de fotos no topo (hero) com troca automática
- Carrossel na seção "Nossa Estrutura" e na seção "Por que escolher a Bem Viver?"
  (com efeito de giro ao passar o mouse), ambos com avanço automático
- Contador de visitas no rodapé (atualiza sozinho quando o site está publicado)
- Formulário de contato com validação, honeypot anti-spam e consentimento LGPD
  obrigatório antes do envio
- SEO: meta tags, Open Graph, dados estruturados Schema.org `LocalBusiness`
- Cabeçalhos de segurança prontos para deploy na Vercel (`vercel.json`)
- Zero dependências de build — é só HTML, CSS e JavaScript puros

---

## 6. Identidade visual

| Uso | Cor |
|---|---|
| Teal principal | `#2F8F80` |
| Teal claro | `#7EC3B6` |
| Teal pálido (fundos suaves) | `#DCF0EC` |
| Teal profundo (rodapé, contrastes) | `#1E5D52` |
| Creme (fundo do site) | `#FAF8F4` |
| Creme quente | `#F1EAE0` |
| Terracota (acentos, CTAs) | `#E2825A` |
| Terracota claro | `#F3BEA0` |

Tipografia: **Cormorant Garamond** (serifada, itálico nos destaques — títulos e
elementos de acolhimento) + **DM Sans** (textos — alta legibilidade).

---

## 7. Segurança (publicando na Vercel)

O arquivo `vercel.json` já vem pronto na pasta com cabeçalhos de segurança
recomendados. Ele é lido automaticamente pela Vercel — não precisa fazer nada,
só subir a pasta `bem-viver` como projeto.

O que esses cabeçalhos fazem:

- **Content-Security-Policy** — só deixa o site carregar scripts, estilos,
  fontes e conexões dos domínios que ele realmente usa (Google Fonts,
  FormSubmit, o contador de visitas e o mapa do Google). Bloqueia qualquer
  script estranho que tente rodar se o site for comprometido por outra via.
- **Strict-Transport-Security** — obriga o navegador a sempre usar HTTPS
  neste domínio depois da primeira visita.
- **X-Frame-Options** — impede que outro site coloque o seu dentro de um
  `<iframe>` (proteção contra clickjacking).
- **X-Content-Type-Options** — impede que o navegador "adivinhe" o tipo de um
  arquivo de forma perigosa.
- **Referrer-Policy** e **Permissions-Policy** — reduzem informação vazada
  para outros sites e desligam câmera/microfone/localização, que o site não usa.

Se um dia adicionar um novo serviço externo (outro formulário, um chat, etc.),
lembre de incluir o domínio dele na lista `connect-src` (ou `frame-src`/`script-src`,
dependendo do caso) dentro do `vercel.json` — senão o navegador vai bloquear
silenciosamente a conexão.

**Boas práticas fora do código** — ative autenticação em duas etapas na conta
da Vercel, do GitHub e no registrador do domínio, e guarde uma cópia de backup
do projeto fora do computador (Google Drive, por exemplo).
