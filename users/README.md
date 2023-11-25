# 📙 Documentação do Agnostic Data Web SDK v1.0.1
O Agnostic Data Web SDK fornece uma série de funções e personalizações que pode ser implementada na captura dos dados para o Agnostic Data que permitem o negócio junto aos desenvolvedores web aplicar eventos específicos para elevar a experiência dos usuários, além de alavancar a compreensão da interação com os consumidores.

# Conteúdo
1. [Variáveis de setup auto-preenchidas](#variáveis-auto-preenchidas-não-modificar)
1. [Eventos Rápidos e Automáticos](#eventos-rápidos-e-automáticos)
1. [Comece pelas meta-tags](#para-a-personalização-comece-pelas-meta-tags)
1. [Personalizando Tracking de Cliques](#elementos-com-prefixo-agnostic_-para-tracking-click-com-contexto)
1. [Rastreamento de Cliques](#rastreamento-de-cliques)
1. [Otimização para análise de conteúdo](#-análise-de-conteúdo-otimizando-as-variáveis-de-controle-automático)
1. [Personalização avançada](#-personalização-avançada-windowagnostica)
1. [ContextFields: enriquecendo as varáveis de contexto](#o-que-são-contextfields)
1. [Links oficiais](#links)

## Variáveis de setup auto-preenchidas (não modificar)
* **sdkVersion**: Esta variável armazena a versão atual do SDK.
* **DEFAULT_APP_INFO_VERSION**: Esta variável deve ser definida durante a compilação e armazena a versão padrão das informações do aplicativo.
* **DEFAULT_APP_PACKAGE_NAME**: Esta variável deve ser definida durante a compilação e armazena o nome do pacote padrão do aplicativo.
* **AG_TOPIC_PRJID**: Esta variável deve ser definida durante a compilação e armazena o nome do tópico PubSub.
* **AG_DB_CLOUD_PROJECT_ID**: Esta variável armazena o ID do projeto do provedor de nuvem.
* **AG_DB_PROJECT_API_KEY**: Esta variável armazena a chave API do projeto.
* **TOKEN_URI**: Esta variável armazena o URI do token.
* **IP_URI**: Esta variável armazena o URI do IP.
* **SCOPE**: Esta variável armazena o escopo do projeto.
* **AVG_SESSION**: Esta variável armazena a duração média da sessão em milissegundos. O valor padrão é 300000 (5 minutos).

## 1️⃣ Eventos Rápidos e Automáticos
Os eventos rápidos e automáticos são pré-definidos para o Agnostic Data Web SDK. Nosso propósito é dar a liberdade e a capacidade de criação de eventos ilimitados para qualquer tipo negócio. No entanto, para acelerar os seus resultados criamos alguns eventos pré-definidos onde você irá começar a capturar imediamente ao implementar o Agnostic Data Web SDK em suas páginas, site ou aplicativo web. 

1. [viewContent](#view_content): evento de visualização de conteúdo é gerado automaticamente quando a página é carregada. 
1. [click](#click): evento de clique. As fontes de cliques podem ser personalizadas.
1. [monitor](#snippet_read-monitor): monitor de área irá verificar se o elemento prefixado com `agnostic-monitor` está (50% mobile ou 70% desktop) visível na tela.
1. [video_status](#video_status): evento de interação de vídeo como youtube, vimeo, pandas video, etc 
1. [form_submitted](#form_submitted): evento de envio de formulário. Se  o atributo agnostic-ignore está aplicado ao formulário o evento será ignorado. 
1. [session_status](#session_status): envia eventos automáticos quando uma sessão é finalizada ou inativa
    1. ended: sessão finalizada (antes de ser fechada ou troca de tab)
    1. inactivated: sessão inativa após 5 minutos
1. [moves](#moves): movimento do mouse durante os primeiros 5 minutos. 

## 2️⃣ Para a personalização comece pelas meta-tags
Resumidamente, meta-tag são elementos html adicionados a uma página web para enriquecer o contexto e fornecer informações para automações, marketing, buscadores, dentre outras finalidades. 

Nosso primeiro exemplo de personalização é o **tempo de sessão**. Sem necessidade de desenvolvedor ou mesmo com pouca experiência, basta adicionar a tag de nome `agnostic_inactivate_minutes` ao seu código e modificar o atributo `content` que representa o tempo em minutos de uma sessão esperada. 

* **agnostic_inactivate_minutes**: Esta meta-tag pode ser usada para definir uma duração de sessão personalizada. O valor deve ser fornecido em minutos. Se o valor fornecido não for um número, a duração da sessão será definida como o valor padrão de 5 minutos.
```html
<meta name="agnostic_inactivate_minutes" content="10">
```

## 3️⃣ Elementos com Prefixo "agnostic_" para tracking click com contexto
Continuando nossa jornada de personalização temos o prefixo `agnostic_` que seleciona todos os elementos cujo id ou class começa com "agnostic_".

Vamos supor que você quer identificar um botão em seu site que tem um papel importante, como um botão de compra. No exemplo abaixo, enviamos automaticamente dentro de um evento `click` o rótulo `postfix_text` `"purchaseButton"`. 
```html
<button id="agnostic_purchaseButton">Comprar Agora</button>
```
ou se tiver utilizando class enviaremos o rótulo `postfix_text` com `"specialOffer"``. 
```html
<button class="agnostic_specialOffer">Oferta Especial</button>
``````
## Rastreamento de Cliques 
Por padrão, automaticamente capturamos os cliques realizados na página e nos elementos `button, a, [id^="agnostic_"], [class^="agnostic_"], input, select, textarea, checkbox, radio, image, img, tab`.

Você pode personalizar uma nova lista de seletores para rastreamento de cliques, incluindo botões, links, elementos com id/class prefixados como "meunegocio_", dentre outros. 

No exemplo abaixo, os valores iniicia, padronizados, dos elementos que serão capturados quando ocorrem clicks estão representados na lista abaixo. O negócio tem a liberdade de modificar essa lista quando quiser e controlar os elementos que enviam originados do evento de clique. 

**Importante**: redefinir o comporamento padrão pode impactar na captura de eventos prefixados com `agnostic_` e deixar de rotular esses eventos. Contudo apesar de não rotular com a valor padrão, uma vez que defina-se um valor como "meunegocio_" é possível extrair alto valor dos eventos. 

`agnostic_click_listeners` padrão: 

```html
<meta name="agnostic_click_listeners" content='button, a, [id^="agnostic_"], [class^="agnostic_"], input, select, textarea, checkbox, radio, image, img, tab'>
```

## 4️⃣ 🚀 Análise de Conteúdo: otimizando as variáveis de controle automático
Essas variáveis permitem uma análise detalhada e personalizada do conteúdo da página, ajudando na tomada de decisões baseadas em eventos e na personalização de experiências de usuário. 

Quando configuradas podem capturar automaticamente sem a necessidade de criar um objeto específico de evento facilitando a vida de times com pouca experiência técnica em desenvolvimento.

Atributos que podem ser personalizados nos campos de contexto: 

1. Tipo de Conteúdo (`agnostic_content_type`)
    
    * **Descrição**: Define o tipo de conteúdo da página (ex: artigo, produto, categoria, teste A/B).
    * **Valor**: Pode ser uma string fixa (ex: "article") ou dinamicamente gerada pelo código baseada no conteúdo da página.
    ```html
    <!-- Exemplo para agnostic_content_type -->
    <meta name="agnostic_content_type" content="article">
    <meta name="agnostic_content_type" content="{{myType}}">
    <!-- Exemplo de uso: Esta meta tag define o tipo de conteúdo da página, por exemplo, um artigo -->
    ```
2. Categoria de Conteúdo (`agnostic_content_category`)
    
    **Descrição**: Especifica a categoria do conteúdo (ex: notícias, esportes, moda, elétrica, hidráulca, protestos, emolumentos) de acordo com a necessidade de cada negócio.
    **Valor**: Pode ser uma string fixa (ex: "news") ou gerada dinamicamente para refletir a categoria do conteúdo da página.
    ```html
    <!-- Exemplo para agnostic_content_category -->
    <meta name="agnostic_content_category" content="news">
    <meta name="agnostic_content_type" content="{{myCategory}}">
    <!-- Exemplo de uso: Esta meta tag define a categoria de conteúdo da página, como notícias -->
    ```    
3. ID do Item (`agnostic_item_id`)
    
    * **Descrição**: Define um identificador único para o item na página, como o ID de um produto ou artigo (ex.: ISBN, SKU, ID de uma campanha, curso, etc).
    * **Valor**: Normalmente numérico e gerado dinamicamente para corresponder ao ID específico do item sendo exibido.
    ```html
    <!-- Exemplo para agnostic_item_id -->
    <meta name="agnostic_item_id" content="{{myID}}">
    <meta name="agnostic_item_id" content="produto-123">
    <!-- Exemplo de uso: Esta meta tag define um ID único para o item na página, como o ID de um produto ou artigo -->
    ```   
4. Nome do Item (`agnostic_item_name`)
    
    * **Descrição**: Define o nome do item na página, como o nome de um produto ou o título de um artigo.
    * **Valor**: Geralmente texto e gerado dinamicamente para refletir o nome real do item em questão.
    ```html
    <!-- Exemplo para agnostic_item_name -->
    <meta name="agnostic_item_name" content="{{productName}}">
    <meta name="agnostic_item_name" content="Nome do Produto">
    <!-- Exemplo de uso: Esta meta tag define o nome do item na página, como o nome de um produto ou o título de um artigo -->    
    ```    
5. Promoção (`agnostic_is_promo`)
    
    * **Descrição**: Indica se o conteúdo é promocional.
    * **Valor**: Pode ser uma string fixa ("true" ou "false") ou determinada dinamicamente com base na natureza do conteúdo.
    ```html
    <!-- Exemplo para agnostic_is_promo -->
    <meta name="agnostic_is_promo" content="true">
    <!-- Exemplo de uso: Esta meta tag define se o conteúdo é promocional -->    
    ```    
6. ID da Promoção (`agnostic_promotion_id`)
    
    * **Descrição**: Define o ID de uma promoção para campanhas de marketing.
    * **Valor**: Pode ser uma string fixa ou gerada dinamicamente para corresponder à promoção específica.
    ```html
    <!-- Exemplo para agnostic_promotion_id -->
    <meta name="agnostic_promotion_id" content="promo123">
    <!-- Exemplo de uso: Esta meta tag define o ID de uma promoção para campanhas de marketing -->    
    ```    
7. Nome da Promoção (`agnostic_promotion_name`)
    
    * **Descrição**: Define o nome de uma promoção para campanhas de marketing.
    * **Valor**: Pode ser uma string fixa ou gerada dinamicamente para corresponder ao nome da promoção.
    ```html
    <!-- Exemplo para agnostic_promotion_name -->
    <meta name="agnostic_promotion_name" content="Promoção de Verão">
    <!-- Exemplo de uso: Esta meta tag define o nome de uma promoção para campanhas de marketing -->    
    ```    
8. Moeda (`agnostic_currency`)
    
    * **Descrição**: Define a moeda usada para quaisquer valores monetários na página.
    * **Valor**: Geralmente uma string fixa representando o código da moeda (ex: "USD", "EUR", "BRL").
    ```html
    <!-- Exemplo para agnostic_currency -->
    <meta name="agnostic_currency" content="BRL">
    <!-- Exemplo de uso: Esta meta tag define a moeda usada para valores na página -->
    ```    
9. Valor (`agnostic_value`)
    
    * **Descrição**: Define o valor monetário associado ao conteúdo, como o preço de um produto. Utilizado também para metrificar resultados de campanhas (ROI), dado que o valor pode ser usado como o valor de cada lead chegar em tal página. 
    * **Valor**: Pode ser fixo ou dinamicamente gerado, especialmente útil para páginas de produtos onde o preço pode variar. 
    * **IMPORTANTE**: existe eventos específicos para capturar o valor de um produto, logo pode-se utilizar a `value` para qualquer finalidade financeira.
    ```html
    <!-- Exemplo para agnostic_value -->
    <meta name="agnostic_value" content="199.99">
    <!-- Exemplo de uso: Esta meta tag define o valor do conteúdo, como o preço de um produto ou o custo de um artigo -->    
    ```    

# 5️⃣ 💪 Personalização avançada: window.agnostica()
A função window.agnostica é utilizada para enviar eventos para o sistema Agnostic Data. Deve-se passar 3 argumentos, sendo eles: nome do evento, dados contextuais e campos específicos do evento.

```javascript
// Recebe o nome do evento, contextFields e specificFields e envia o fluxo onde:
// contextFields: user_id, user_pseudo_id, user_phone, userToken, is_promo, items
// specificFields: campos específicos do evento com validação. Veja a documentação. 
// Ex.: {product_id: 123, product_name: "produto 1"}

let contextFields = {}
let specificFields = {}
window.agnostica("event_name", contextFields, specificFields)
```

Aqui está um exemplo de evento que podem ser enviados usando a `agnostica`. *Contudo, neste caso, esse evento já é enviado automaticamente quando o usuário clica em um elemento na interface do usuário*. Aqui hipoteticamente, vamos usá-lo para representer um envio manual utilizando o **sdk**.
```javascript
window.agnostica('click', contextFields, specificFields);
```
* `contextFields`: Este objeto contém informações contextuais sobre o evento, como o ID do usuário (veja na seção "ContextFields Enriquecendo as varáveis de contexto")
* `specificFields`: Este objeto contém informações específicas sobre o evento, como o ID do elemento clicado, o texto do elemento clicado, e outros atributos previamente esperados (veja mais em Console => Catalog).

## O que são contextFields?
Os `contextFields` dão contexto ao evento e compõe o payload. 
```javascript
    let event = {
        ...contextFields,
        event_data: [{ ...specificFields }],
    };
```

### ContextFields: enriquecendo as varáveis de contexto
Você pode enriquecer as variáveis de contexto, modificando os atributos de contextFields de acordo com a necessidade. Abaixo descrevemos essas variáveis que podem ser enriquecidas, neste exemplo quando na WEB.

    **IMPORTANTE**: não altere a variável **scope** e nenhuma das variáveis na seção **Variáveis auto-preenchidas 
    (não modificar)**, pois a solução poderá parar de capturar e o projeto ser bloqueado automaticamente.

Seguem exemplos de uso dos campos de contexto, denominados contextFields, que podemos alterar e escolher valores no Agnostic Data Web SDK:

- `event_provider?: Nullable<string>`(@future indisponivel no momento)
    * **Descrição:** O fornecedor do evento para o marketplace, caso seja um evento criado por outros provedores 
    * **Tipo:** String ou `null`.

- `app_info_version: string`
    * **Descrição:** A versão do seu app ou site. 
    * **Exemplo:** "tom-4.0.1" ou "web-4.0.1" ou "presto-4.0.1".

- `app_package_name: Nullable<string>`
    * **Descrição:** Nome do pacote ou site.     
    * **Tipo:** String ou `null`.
    * **Exemplo:** "com.agnosticdata.app" ou URL.
    * **Comportamento**: 💡 quando na web irá automaticamente capturar `window.location.hostname` (url do site sem caminhos relativos); quando não informado irá buscar a definição padrão realizada na Console => Project => Settings. 

- `relative_view?: Nullable<string>`  
    * **Descrição:** Usado para conter page_view e screen_view relativa 
    * **Tipo:** String ou `null`.
    * **Exemplo:** "domain.com/relativeURL/relativeAgain" ou "com.lovyca.app.relativeURL".
    * **Comportamento**: 💡 na web é automaticamente capturada por `window.location.pathname` (caminho relativo do site). Em mobile a cada view carregada chame o evento (ex.: onRender)

-  `user_id` (Default: Null)
    * **Tipo:** `Nullable<string>`
    * **Descrição:** Identificador único do usuário. Se não for informando será null.
    * **Exemplo:** `12345abcde`

- `user_phone` (Default: Null)
    * **Tipo:** `Nullable<string>`
    * **Descrição:** Número de telefone do usuário. Se não for informando será null.

- `userToken` (Default: Null)
    * **Tipo:** `Nullable<string>`
    * **Descrição:** Token do usuário, usado para serviços específicos como Algolia. Se não for informando será null.

- `is_promo`
    * **Tipo:** `Nullable<boolean>`
    * **Descrição:** Indica se o evento está relacionado a uma promoção. Recuperado da meta-tag is_promo. Se não for informando será null.

- `items`
    * **Tipo:** `Array[]`
    * **Descrição:** lista de itens com estrutura pré-definda conforme "Estrutura de um Item" a seguir.


#### Estrutura de um Item
Segue a estrutura de um item que pode ser adicionado na Array items do contextFields do tópico "Enriquecendo as varáveis de contexto". Lembre-se que os itens sem a interroção (?) no final da declaração do nome são obrigatórios, como `id, quantity, value, discount, etc`. Os campos com Nullable podem ser passados como `null` ou o `<tipo>` definido.

```typescript
export interface Item {
  index?: Nullable<number>;
  id: string;
  item_id?: Nullable<string>;
  item_name?: Nullable<string>;
  lisn_department?: Nullable<string>;
  lisn_section?: Nullable<string>;
  lisn_item?: Nullable<string>;
  quantity: number;
  currency?: Nullable<string>;
  value: Nullable<number>;
  discount: Nullable<number>;
  price?: Nullable<number>;
  item_category?: Nullable<string>;
  item_category2?: Nullable<string>;
  item_list_name?: Nullable<string>;
  item_list_id?: Nullable<string>;
  location_id?: Nullable<string>;
  coupon?: Nullable<string>;
  affiliation?: Nullable<string>;
  promotion_id?: Nullable<string>;
  promotion_name?: Nullable<string>;
}
```

# SpecificFields: Eventos
Os campos específicos são campos contidos especificamene em cada evento. Eles são validados durante o processamento, logo cada evento chamado em agnostic("event_name", ... ,  specificFields) tem sua própria estrutura e comporamento. Para saber mais sobre o conteúdo dos eventos acesso a console e navegue no catálogo. 

## view_content
```javascript
    const event = {
        event_type: 'view_content',
        content_name: document.title || 'none', // from page title
        content_type: agnostic_content_type, // from meta-tag
        item_id: variables.agnostic_item_id, // from meta-tag
        item_name: variables.agnostic_item_name, // from meta-tag
        promotion_id: variables.agnostic_promotion_id, // from meta-tag
        promotion_name: variables.agnostic_promotion_name, // from meta-tag
        currency: variables.agnostic_currency, // from meta-tag
        value: variables.agnostic_value ? Number(variables.agnostic_value) : null, // from meta-tag
        content_category: variables.agnostic_content_category, // from meta-tag
        utm_source: variables.utm_source, // from utm
        utm_medium: variables.utm_medium, // from utm
        utm_campaign: variables.utm_campaign, // from utm
        utm_id: variables.utm_id, // from utm
        utm_term: variables.utm_term, // from utm
        utm_content: variables.utm_content, // from utm
        fbclid: variables.fbclid 
    }

```

## click
```javascript
        const event = {
            ui_event_type: 'click',
            element_type: targetElement.tagName, // from click
            view_content_name: document.title || 'none'), // from title
            element_label: element_label || 'none'), 
            alt_text: alt_text, // alt text of element
            view_content_type: variables.agnostic_content_type, // from meta-tag
            x: event.clientX, // x position
            y: event.clientY, // y position
            // remove prefix agnostic_ from id and clas
            postfix_text: postfix_text
        }
```
## snippet_read (monitor)
```javascript
        const event = {
            content_name: document.title || 'none', // from page title
            content_type: variables.agnostic_content_type, // from meta-tag
            target_id: entry.target.id || null,
            class_name: entry.target.className || null,
            utm_source: variables.utm_source, // from utm
            utm_medium: variables.utm_medium, // from utm
            utm_campaign: variables.utm_campaign, // from utm
            utm_id: variables.utm_id, // from utm
            utm_term: variables.utm_term, // from utm
            utm_content: variables.utm_content, // from utm
            fbclid: variables.fbclid
        }
```

## video_status
```javascript
        const event = {
            content_name: document.title || 'none'  // from page title
            content_type: variables.agnostic_content_type, // from meta-tag
            status: 'play',
            video_id: video.id || null,
            video_name: video.name || null,
            video_duration: video.duration || null,
            video_current_time: video.currentTime || null,
            video_volume: video.volume || null,
            video_playback_rate: video.playbackRate || null,
            video_src: video.src || null,
        }
```

## form_submitted
```javascript
        const event = {
            content_name: document.title || 'none'  // from page title
            content_type: variables.agnostic_content_type, // from meta-tag
            form_id: form.id || null,
            form_name: form.name || null,
            form_action: form.action || null,
            form_payload: form_payload
        }
```
## session_status
```javascript
        const session_inactivated = {
            content_name: document.title || 'none', // page title
            content_type: variables.agnostic_content_type, // from meta-tag
            currency: variables.agnostic_currency,
            value: variables.agnostic_value ? Number(variables.agnostic_value) : null,
            duration: Date.now() - INIT_SESSION,
            status: 'inactivated', // ou ended
            utm_source: variables.utm_source, // from utm
            utm_medium: variables.utm_medium, // from utm
            utm_campaign: variables.utm_campaign, // from utm
            utm_id: variables.utm_id, // from utm
            utm_term: variables.utm_term, // from utm
            utm_content: variables.utm_content, // from utm
            fbclid: variables.fbclid 
        }
```
## moves
```javascript
        const event = {
            content_name: content_name: document.title || 'none', // page title
            content_type: content_type: variables.agnostic_content_type, // from meta-tag
            moves: moves, // mouse moving
            duration: sessionDuration
        }
```

## Miscelânea

### FBClid
Você pode atribuir um fbclid (Facebook Pixel id a um evento) via querystring fbclid=IDFBCLID. Contudo lembre-se que Facebook é um *destination* e precisa ser configurado API_KEY e INSTANCE_ID nessas configurações. 

# Links
Para informações adicionais acesse:
* https://www.agnosticdata.ai/
* https://docs.agnosticads.com/
