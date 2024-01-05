# 📙 Documentação do Agnostic Data Web SDK v1.0.1
O Agnostic Data Web SDK fornece uma série de funções e personalizações que pode ser implementada na captura dos dados para o Agnostic Data que permitem o negócio junto aos desenvolvedores web aplicar eventos específicos para elevar a experiência dos usuários, além de alavancar a compreensão da interação com os consumidores.

# Conteúdo
1. [Eventos Rápidos e Automáticos](#1%EF%B8%8F⃣-eventos-rápidos-e-automáticos)
1. [Comece pelas meta-tags](#2%EF%B8%8F⃣-para-a-personalização-comece-pelas-meta-tags)
1. [Como otimizar para análise de conteúdo](#3%EF%B8%8F⃣--análise-de-conteúdo-como-otimizar-as-variáveis-de-controle-automático)
1. [Personalizando Tracking de Cliques](#4%EF%B8%8F⃣-elementos-com-prefixo-agnostic_-para-tracking-click-com-contexto)
1. [Rastreamento de Cliques](#4%EF%B8%8F⃣-elementos-com-prefixo-agnostic_-para-tracking-click-com-contexto)
1. [Personalização avançada](#6%EF%B8%8F%E2%83%A3--personaliza%C3%A7%C3%A3o-avan%C3%A7ada-windowagnostica)
    1. [ContextFields: enriquecendo as varáveis de contexto](#contextfields-enriquecendo-as-varáveis-de-contexto)
1. [SpecificFields: Eventos](#7%EF%B8%8F⃣-%EF%B8%8F-specificfields-eventos)
    1. [view_content](#view_content)
    1. [sign_up](#sign_up)
    1. [checkout_init](#checkout_init)
    1. [checkout_done](#checkout_done)
1. [Complete data (complete_data)](#complete-data-complete_data)
    1. [Exemplo no backend (Complete Data): complete_data](#exemplo-no-backend-complete-data-complete_data)
    1. [Utilizando o agnostica.identify()](#utilizando-o-agnosticaidentify)
1. [Links oficiais](#links)
1. [Variáveis de setup auto-preenchidas](#variáveis-auto-preenchidas-não-modificar)
1. [Hacks - Medir custo por lead](#hacks)
1. [Carga de links](#carga-de-links)

## 1️⃣ Eventos Rápidos e Automáticos
Os eventos rápidos e automáticos são pré-definidos para o Agnostic Data Web SDK. Nosso propósito é dar a liberdade e a capacidade de criação de eventos ilimitados para qualquer tipo negócio. No entanto, para acelerar os seus resultados criamos alguns eventos pré-definidos onde você irá começar a capturar imediamente ao implementar o Agnostic Data Web SDK em suas páginas, site ou aplicativo web. 

1. [viewContent](#view_content): evento de visualização de conteúdo é gerado automaticamente quando a página é carregada. É o evento mais fácil e rápido para aprender sobre a jornada de conversão. Veja mais em [Análise de Conteúdo: como otimizar as variáveis de controle automático](#3%EF%B8%8F⃣--análise-de-conteúdo-como-otimizar-as-variáveis-de-controle-automático) 
1. [click](#click): evento de clique. As fontes de cliques podem ser personalizadas.
1. [monitor](#snippet_read-monitor): monitor de área irá verificar se o elemento prefixado com `agnostic-monitor` está (50% mobile ou 70% desktop) visível na tela.
1. [video_status](#video_status): evento de interação de vídeo como youtube, vimeo, pandas video, etc 
1. [form_submitted](#form_submitted): evento de envio de formulário. Se  o atributo agnostic-ignore está aplicado ao formulário o evento será ignorado. 
1. [session_status](#session_status): envia eventos automáticos quando uma sessão é finalizada ou inativa
    1. ended: sessão finalizada (antes de ser fechada ou troca de tab)
    1. inactivated: sessão inativa após 5 minutos
1. [moves](#moves): movimento do mouse durante os primeiros 5 minutos. 

* **IMPORTANTE**: `apid` significa Agnostic Pixel Id, quando definido como variável em uma querystring ele irá passar para os eventos a. session_status, b. snippet_read e c. view_content o atributo `apid` dentro do `event_data`.

## 2️⃣ Para a personalização comece pelas meta-tags
Resumidamente, meta-tag são elementos html adicionados a uma página web para enriquecer o contexto e fornecer informações para automações, marketing, buscadores, dentre outras finalidades. 

Nosso primeiro exemplo de personalização é o **tempo de sessão**. Sem necessidade de desenvolvedor ou mesmo com pouca experiência, basta adicionar a tag de nome `agnostic_inactivate_minutes` ao seu código e modificar o atributo `content` que representa o tempo em minutos de uma sessão esperada. 

* **agnostic_inactivate_minutes**: Esta meta-tag pode ser usada para definir uma duração de sessão personalizada. O valor deve ser fornecido em minutos. Se o valor fornecido não for um número, a duração da sessão será definida como o valor padrão de 5 minutos.
```html
<meta name="agnostic_inactivate_minutes" content="10">
```

## 3️⃣ 🚀 Análise de Conteúdo: como otimizar as variáveis de controle automático
Acelere o aprendizado dos eventos do seu site, aplicativo ou página. Defina as meta-tags abaixo e otimizande seus resultados. 

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
    * **IMPORTANTE**: se a variável de querystring `cc` for passada na URL ela irá prevalecer contra `agnostic_currency`
9. Valor (`agnostic_value`): null ou Number
    
    * **Descrição**: Define o valor monetário associado ao conteúdo, como o preço de um produto. Utilizado também para metrificar resultados de campanhas (ROI), dado que o valor pode ser usado como o valor de cada lead chegar em tal página. 
    * **Valor**: Pode ser fixo ou dinamicamente gerado, especialmente útil para páginas de produtos onde o preço pode variar. 
    * **IMPORTANTE**: existe eventos específicos para capturar o valor de um produto, logo pode-se utilizar a `value` para qualquer finalidade financeira.
    ```html
    <!-- Exemplo para agnostic_value -->
    <meta name="agnostic_value" content="199.99">
    <!-- Exemplo de uso: Esta meta tag define o valor do conteúdo, como o preço de um produto ou o custo de um artigo -->    
    ```    
    * **IMPORTANTE**: se a variável de querystring `vv` for passada na URL ela irá prevalecer contra `agnostic_value`
## 4️⃣ Elementos com Prefixo "agnostic_" para tracking click com contexto
Continuando nossa jornada de personalização temos o prefixo `agnostic_` que seleciona todos os elementos cujo id ou class começa com "agnostic_".

Vamos supor que você quer identificar um botão em seu site que tem um papel importante, como um botão de compra. No exemplo abaixo, enviamos automaticamente dentro de um evento `click` o rótulo `postfix_text` `"purchaseButton"`. 
```html
<button id="agnostic_purchaseButton">Comprar Agora</button>
```
ou se tiver utilizando class enviaremos o rótulo `postfix_text` com `"specialOffer"``. 
```html
<button class="agnostic_specialOffer">Oferta Especial</button>
```

## 5️⃣ Rastreamento de Cliques 
Por padrão, automaticamente capturamos os cliques realizados na página e nos elementos `button, a, [id^="agnostic_"], [class^="agnostic_"], input, select, textarea, checkbox, radio, image, img, tab`.

Você pode personalizar uma nova lista de seletores para rastreamento de cliques, incluindo botões, links, elementos com id/class prefixados como "meunegocio_", dentre outros. 

No exemplo abaixo, os valores iniicia, padronizados, dos elementos que serão capturados quando ocorrem clicks estão representados na lista abaixo. O negócio tem a liberdade de modificar essa lista quando quiser e controlar os elementos que enviam originados do evento de clique. 

**Importante**: redefinir o comporamento padrão pode impactar na captura de eventos prefixados com `agnostic_` e deixar de rotular esses eventos. Contudo apesar de não rotular com a valor padrão, uma vez que defina-se um valor como "meunegocio_" é possível extrair alto valor dos eventos. 

`agnostic_click_listeners` padrão: 

```html
<meta name="agnostic_click_listeners" content='button, a, [id^="agnostic_"], [class^="agnostic_"], input, select, textarea, checkbox, radio, image, img, tab'>
```


# 6️⃣ 💪 Personalização avançada: adai.event()
A função adai.event é utilizada para enviar eventos para o sistema Agnostic Data. Deve-se passar 3 argumentos, sendo eles: nome do evento, dados contextuais e campos específicos do evento.

```javascript
// Recebe o nome do evento, contextFields e specificFields e envia o fluxo onde:
// contextFields: user_id, user_pseudo_id, user_phone, userToken, is_promo, items
// specificFields: campos específicos do evento com validação. Veja a documentação. 
// Ex.: {product_id: 123, product_name: "produto 1"}

let contextFields = {}
let specificFields = {}
adai.event("event_name", contextFields, specificFields)
```

* **IMPORTANTE**: se a variável de querystring `apsid` for passada na URL ela irá prevalecer contra `pseudo_id` auto-gerado. 

Aqui está um exemplo de evento que podem ser enviados usando a `agnostica`. *Contudo, neste caso, esse evento já é enviado automaticamente quando o usuário clica em um elemento na interface do usuário*. Aqui hipoteticamente, vamos usá-lo para representer um envio manual utilizando o **sdk**.
```javascript
adai.event('click', contextFields, specificFields);
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


#### Estrutura de um Item (items[])
Segue a estrutura de um item que pode ser adicionado na Array items do contextFields do tópico "Enriquecendo as varáveis de contexto". Lembre-se que os itens sem a interroção (?) no final da declaração do nome são obrigatórios, como `id, quantity, value, discount, etc`. Os campos com Nullable podem ser passados como `null` ou o `<tipo>` definido.

```typescript
export interface Item {
  id: string;
  quantity: number;
  value: Nullable<number>;
  discount: Nullable<number>;
  index?: Nullable<number>;
  item_id?: Nullable<string>;
  item_name?: Nullable<string>;
  lisn_department?: Nullable<string>;
  lisn_section?: Nullable<string>;
  lisn_item?: Nullable<string>;
  currency?: Nullable<string>;
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

# 7️⃣ ✈️ SpecificFields: Eventos
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

## sign_in 
```javascript

    const event = {
        method: SignupMethodType
    }

    type SignupMethodType =
    | "facebook"
    | "google"
    | "email_password"
    | "phone_sms"
    | "email_link"
    | "appleid"
    | "twitter"
    | "linkedin"
    | "instagram"
    | "amazon"
    | "microsoft"
    | "github"
    | "federated"

```

### Chamada no navegador
```javascript
     // try
     adai.event("sign_in", 
        null, 
        {
            method: "phone_sms",
            step: "try" // || "done"; // represents the step of the event try auth or done auth
            // info?: Nullish<string> // custom info about method
            // method_type?: Nullish<string>;  // custom method like others if method not provides         
        });
     // SE done é preciso passar user_id
     adai.event("sign_in", 
        {"user_id": "usuarioautenticadotemid"}, 
        {
            method: "phone_sms",
            step: "done"; // represents the step of the event try auth or done auth
            // info?: Nullish<string> // custom info about method
            // method_type?: Nullish<string>;  // custom method like others if method not provides         
        });  
    // IMPORTANTE: use agnostica.identify ou adai.identify após um usuário autenticado para correlacionar
    // informações
    agnostica.identify("horaciodasilvamoreira", {"email": "horacio@gmail.com", "phone": "61999931122", "firstname": "Horacio"})
    // feito isso não precisa enviar user_id nos eventos que exigem esse campo preenchido
    // por exemplo, após rodar adai.identify() o sign_in do tipo "done" não precisa de user_id
    // done
    adai.event("sign_in", 
        null,
        {
            method: "phone_sms",
            step: "done"; // represents the step of the event try auth or done auth
            // info?: Nullish<string> // custom info about method
            // method_type?: Nullish<string>;  // custom method like others if method not provides         
        });      
      
```

## sign_up 
registro de entrada no sistema/app

**Atributos do event_data:**
| Nome do Atributo     | Obrigatório | Descrição                                     |
|-----------------------|-------------|-----------------------------------------------|
| method                  | Sim        |  Método de autenticação SignupMethodType |
| content_name             | Sim         | Título da página  |
| content_type              | Sim         | Tipo da página para test A/B  |
| status      | Sim (number)         | Inteiro representando o status deste usuário. Ex.: 1 aitvo ou 0 inativo  |
| currency      |  Nulo ou String         | Nulo ou string com a moeda BRL, USD, etc|
| value      | NUlo ou Inteiro         | Nulo ou valor em inteiro. Não passe 0 se não tiver valor. Essa informação é utilizar para apurar o valor de um signup pelo time de marketing, por exemplo.  |
| step       | Sim     | Valores: try ou done (String) representam o clique para tentar o evento e done se deu tudo certo no request e registro (signu_up) |
| info       | Não     | Espaço para informação adicional a este evento (String) |


```javascript

    const event = {
        method: SignupMethodType;
        content_name: string; // Signup Tomador, Signup Prestador, Signup CaaS, Signup Whatsapp
        content_type: string; // Taxonomy sheet
        status: number; // default 1 or status after registration
        step: "try" || "done"; // represents the step of the event try auth or done auth
        info?: Nullish<string>; // custom info about method        
        currency: Nullable<string>; // relates to value
        value: Nullable<number>; // value or cost of event
    }

    type SignupMethodType =
    | "facebook"
    | "google"
    | "email_password"
    | "phone_sms"
    | "email_link"
    | "appleid"
    | "twitter"
    | "linkedin"
    | "instagram"
    | "amazon"
    | "microsoft"
    | "github"
    | "federated"

```

### Chamada no navegador
```javascript

     // try
     adai.event("sign_up", 
        null, 
        {
            method: "phone_sms", 
            content_name: "Sign_up | Resolve",  // Geralmente <Title>
            content_type: "sign_up-a",  // sign_up-A , versão A de A/B
            step: "try" // 1st clique to auth or "done" if success authenticated
            status: 1,  // Status do usuário após o Sign-up, geralmente 1
            info: "optional info"
            currency: null, // string ou null, geralmente BRL
            value: null // nulo, mas se informado deve inteiro
        });
     // Se done
     adai.event("sign_up", 
        {"user_id": "usuarioautenticadotemid"},
        {
            method: "phone_sms", 
            content_name: "Sign_up | Resolve",  // Geralmente <Title>
            content_type: "sign_up-a",  // sign_up-A , versão A de A/B
            step: "done" // 1st clique to auth or "done" if success authenticated
            status: 1,  // Status do usuário após o Sign-up, geralmente 1            
            info: "optional info"
            currency: null, // string ou null, geralmente BRL
            value: null // nulo, mas se informado deve inteiro
        });        
      
    // IMPORTANTE: use agnostica.identify ou adai.identify após um usuário autenticado para correlacionar
    // informações
    agnostica.identify("horaciodasilvamoreira", {"email": "horacio@gmail.com", "phone": "61999931122", "firstname": "Horacio"})
    // feito isso não precisa enviar user_id nos eventos que exigem esse campo preenchido
    // por exemplo, após rodar adai.identify() o sign_in do tipo "done" não precisa de user_id
    // done
     adai.event("sign_up", 
        null,
        {
            method: "phone_sms", 
            content_name: "Sign_up | Resolve",  // Geralmente <Title>
            content_type: "sign_up-a",  // sign_up-A , versão A de A/B
            step: "done" // 1st clique to auth or "done" if success authenticated
            status: 1,  // Status do usuário após o Sign-up, geralmente 1            
            info: "optional info"
            currency: null, // string ou null, geralmente BRL
            value: null // nulo, mas se informado deve inteiro
        });        

```

## sign_out
```javascript
    // Interface
    interface event = {
        step: "try" | "done"; // "start" or "end
        info?: Nullish<string> // custom info about method
    }
    // COM try
     adai.event("sign_out", 
        {"user_id": "usuarioautenticadotemid"},
        {
            step: "try" // 1st clique to auth or "done" if success authenticated
        });  
    // COM done
     adai.event("sign_out", 
        null,
        {
            step: "done" // 1st clique to auth or "done" if success authenticated
        });
```

### Chamada no navegador
```javascript

     adai.event("sign_out", 
        null, 
        {
            step: "try" || "done"; // represents the step of the event try auth or done auth
            info?: Nullish<string> // custom info about method
        });
      
```


## checkout_init
utilizado quando uma pessoa entra no fluxo de finalização da compra antes de concluí-lo, por exemplo, uma pessoa clica em um botão de finalização da compra. Para integração automática com Google Analytics use items no corpo do evento. 

**Atributos do event_data:**
| Nome do Atributo     | Obrigatório | Descrição                                     |
|-----------------------|-------------|-----------------------------------------------|
| step                  | Não         | utilizado para adicionar uma string informativa como added_address, added_paymentInfo, selected_paymentOption
| value                 | Não         | Se passado deve ser inteiro onde 4.90 será 490
| currency              | Não         | Default 'BRL', se passado deve ser string                         |
| content_category      | Não         | Categoria do item (categoria do ecommerce, do tipo de produto, etc)                          |


Observação: para este evento funcionar de forma integrada com o Google Analytics é necessário passar items no corpo do evento `events.items`, além do `events.event_data`. Caso o atributo items não seja preenchido adequadamente, o evento no Agnostic Data será registrado, porém no Google Analytics levantará uma exceção isolado para esse destino, caso seu produto/serviço use Google Analytics, considere inserir items, conforme o exemplo abaixo (opacao 1). 

### Chamada no navegador
```javascript
    // opcao 1 (recomendada para integração automática com GA)
    // se R$ 197.00
    // adai.event(event_name, context_fields, event_data)
    // onde 
    // context_fields neste caso é necessário apenas items
    // event_data utilizar os campos da tabela acima conforme necessidade
     adai.event("checkout_init", 
        {items: [{id: "NR_CHAVE", quantity: 1, value: 19700, discount: null}]}, 
        {step: "added_address", value: 20450, content_category: "título" });

    // opcao 2 (sem items)
    // se R$ 197.00
     adai.event("checkout_init", 
        null, 
        {step: "added_address", value: 20450, content_category: "título" });        

```

### Campos obrigatórios de um item
Um item é uma estrutura para depositar um item de compra, de seleção, como um SKU, um produto ou um serviço. Em um evento items pode ser passado como null, como `event.items = null`, contudo caso tenha items, para total integração com GA, convém que os valores sigam este padrão. Os campos obrigatórios são:

* id: string;
* quantity: number;
* value: number;
* discount: number || null;

*Obs: Veja em "Estrutura de um Item (items[])" mais detalhes sobre o conteúdo de um item.* 


## checkout_done
utilizado quando o usuário finaliza definitivamente uma compra, pagamento completado. Pode-se chamar do lado do servidor ou do lado do cliente.

**Atributos do event_data:**

  * content_name: string; // page/view title
  * content_type: string; // Page_Category_A or Page_Category_B (for test and subcategory)
  * currency: string;
  * value: number;
  * tid: string;
  * status?: Nullish<string>;
  * coupon?: Nullish<string>;
  * shipping?: Nullish<number>;
  * tax?:Nullish<number>;


| Nome do Atributo     | Obrigatório | Descrição                                     |
|-----------------------|-------------|-----------------------------------------------|
| content_name | Sim         | Título da página |
| content_type | Sim         | Utilizado para test A/B ou definir um subtito de página|
| currency     | Sim         | Default 'BRL', se passado deve ser string                         |
| value      | Sim         | Valor em inteiro 3.99 deve ser passado 399     |
| tid      | Sim         | identificador único da transacao |
| status      | Não         | status da transação, de livre preenchimento. ex.: "processing", "done" |
| coupon      | Não         | um string contendo o código de cupom |
| shipping      | Não         | Não definido, nulo ou valor em inteiro 3.99 deve ser passado 399   |
| tax      | Não         | Não definido, nulo ou valor em inteiro 3.99 deve ser passado 399     |

Observação: para este evento funcionar de forma integrada com o Google Analytics é necessário passar items no corpo do evento `events.items`, além do `events.event_data`. Caso o atributo items não seja preenchido adequadamente, o evento no Agnostic Data será registrado, porém no Google Analytics levantará uma exceção isolado para esse destino, caso seu produto/serviço use Google Analytics, considere inserir items, conforme o exemplo abaixo (opacao 1). 

### Chamada no navegador
```javascript
    // opcao 1 (recomendada para integração automática com GA)
    // se R$ 197.00
    // adai.event(event_name, context_fields, event_data)
    // onde 
    // context_fields neste caso é necessário apenas items
    // event_data utilizar os campos da tabela acima conforme necessidade
     adai.event("checkout_done", 
        {items:[{id: "NR_CHAVE", quantity: 1, value: 19700, discount: null}]}, 
        {  content_name: "Payment Page", content_type: "Payment-Page-V1", value: 20450, currency: "BRL", 
            value: 399, tid: "Ad0CiCAM3uaM0R01", status: "payment_done", tax: 750  });
```

### Chamada no backend com encodeEvent (payload do cliente)
É importante destacar que a estratégia de envio futuro de um evento aplica-se a casos que o negócio precisa entender dados do ambiente do cliente em conjunto com dados da evitivação da transação. Como algumas transações são assíncronas como pagamento de Pix e Boleto a informação de `pagamento efetivado` pode vir tardiamente quando o usuário não está mais na sessão. Para esses, casos podemos usar o post-message, o envio do evento em momento futuro. 

```javascript
    // Passo 1: Frontend com Post-message envie o payload do evento capturado no frontend ao backend
        
        // Para gerar uma payload do evento para envio futuro, atribua true ao `for_future_use` em window.agnostic
        // ex.: adai.event(event_name, context_fields, event_payload, true)
        const IS_FUTURE = true
        // capturar encodeEvent
        const { encodeEvent } = await adai.event("checkout_done", 
                                        {items:[{id: "NR_CHAVE", quantity: 1, value: 19700, discount: null}]}, 
                                        {content_name: "Payment Page", content_type: "Payment-Page-V1", value: 20450, currency: "BRL", 
                                        value: 399, tid: "Ad0CiCAM3uaM0R01", status: "payment_done_future", tax: 750  }, 
                                        IS_FUTURE); 
        // no seu evento de frontend, envie encodeEvent para o backend e mantenha-o até o callback de pagamento efetivado
        // "Pagar" () => sendRequest(encodeEvent) 
    
    // Passo 2: No backend, use sua melhor escolha para submeter um POST do evento passando encodeEvent
    //  
        const response = await fetch(TOKEN_URI); // token expira a cada uma 1 hora, solicitações em excesso no intervalo menor que 1h pode ser bloqueada.
        const {token, expires_in} = await response.json()
        const API_URL = `https://pubsub.googleapis.com/v1/projects/${AG_DB_CLOUD_PROJECT_ID}/topics/${AG_TOPIC_PRJID}:publish`;
        const response = await fetch(API_URL, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${token}`,
            "Content-Type": "application/json",
        },
        body: JSON.stringify({
            messages: [
                {
                    data: encodeEvent,
                },
            ],
        }),
    });
```

### Chamada no backend sem encodeEvent (evento completo)
```javascript
    /// Exemplo no backend
    // Passo 2: No backend, use sua melhor escolha para submeter um POST do evento passando encodeEvent
    //  
        const response = await fetch(TOKEN_URI); // token expira a cada uma 1 hora, solicitações em excesso no intervalo menor que 1h pode ser bloqueada.
        const {token, expires_in} = await response.json()
        const API_URL = `https://pubsub.googleapis.com/v1/projects/${AG_DB_CLOUD_PROJECT_ID}/topics/${AG_TOPIC_PRJID}:publish`;
        const response = await fetch(API_URL, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${token}`,
            "Content-Type": "application/json",
        },
        body: JSON.stringify({
        messages: [{ data: 
                Buffer.from(JSON.stringify({
                    created: Math.floor(Date.now() / 1000), // timestamp in seconds
                    event_name: "checkout_done",
                    scope: "MY_KEY:MY_PROJECT_ID",
                    app_info_version: "backend-v1",
                    action_source: "system_generated",
                    user_id: null, // user da transacao 
                    user_phone: null, // telefone de user se disponivel na transacao                    
                    // event_type: null, 
                    // event_name_from_type: null, 
                    // carrier: null, 
                    // user_pseudo_id: null, 
                    // userToken: null, 
                    // is_promo: null,
                    // device_brand: null,
                    // device_resolution: null,
                    // device_screen_density: null,
                    // device_so: null,
                    // device_so_version: null,
                    // device_language: null,
                    // device_model_name: null, // * iPhone 11
                    // device_web_browser: null, // client_user_agent
                    // device_ipaddress: null,
                    // device_geohash: null,
                    // device_timezone: null, //* America/Sao_Paulo:GMT-3
                    // opened_from_type: null, // external_link, deep_link, push_notification, null (referrer)
                    // opened_from_content: null,
                    // geodata: null,
                    // target_data: [],
                    items: [{id: "NR_CHAVE 2", quantity: 1, value: 20000, discount: 100}],
                    event_data: [
                        {   
                            content_name: "Payment Page 2", 
                            content_type: "Payment-Page-V2", 
                            value: 20450, 
                            currency: "BRL", 
                            tid: "Ad0CiCAM3uaM0R01", 
                            status: "payment_done", 
                            // coupon: null,
                            // shipping: null,
                            tax: 750
                        }
                    ]
                })).toString("base64")
            }],        
        })
    });    
```

### Campos obrigatórios de um item
Um item é uma estrutura para depositar um item de compra, de seleção, como um SKU, um produto ou um serviço. Em um evento items pode ser passado como null, como `event.items = null`, contudo caso tenha items, para total integração com GA, convém que os valores sigam este padrão. Os campos obrigatórios são:

* id: string;
* quantity: number;
* value: number;
* discount: number || null;

*Obs: Veja na seção ["Estrutura de um Item (items[])"](https://github.com/horacioibrahim/docs.agnosticdata/blob/main/users/README.md#estrutura-de-um-item-items) mais detalhes sobre o conteúdo de um item.*


## click
```javascript
        const event = {
            ui_event_type: 'click',
            element_type: targetElement.tagName, // from click
            view_content_name: document.title || 'none', // from title
            element_label: element_label || 'none', 
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

## Veja também neste documento
    * pixel_request
    * redirect_request
    * carga de pixel links
    * carga de redirect links (shorten)


# Hacks
## Como definir o valor por fonte, tipo de lead, campanha ou condicionais
No Agnostic Data Web SDK é possível definir `agnostic_value` de forma condional basedo em parâmetros da url (as querystring). Ajuste seu arquivo de configuração na console ou diretamente no JSON aplicando as regras em `settings.agnostic_values`. Veja como é simples.

No exemplo temos:
- Dado que temos uma variável na url chamada `utm_content`
- e que o valor dessa variáel é `news`
- então o valor deste acesso será 0.23 centavos que DEVE ser aplicado como inteiro, ou seja, `23`. 

```json
{// config.json file
    ...
    "settings": {
        "agnostic_values": [
            {
                "qfield": "utm_content", // field for match into querystring
                "qvalue": "news", // value for compare
                "agnostic_value": 23 // integer where 0.23 is 23
            }
        ]
    }
}
```

# Carga de links
Contém o modelo para envio de links para redicionamento limitado a 500 links por POST.

```json
{
    "links": [
            {
            "project_id": "agnostic-saas-01",
            "scope": "MY_KEY:MY_PROJECT_ID",
            "user_id": "123456",
            "is_active": true,
            "domain_short": "rslv.cc",
            "url_target": "mydomain-gigante.meusetor.minhaempresa.com.br",
            "hash": "primeira",
            "redirect_to": "https://homolog.resolve.cenprot.org.br",
            "status": "created",
            "apsid": "pseudo---123456",
            "acid": "usuario-from-customer",
            "apid": "pixel-i781279123",
            "utm_source": "cenprot",
            "utm_medium": "email",
            "utm_campaign": "topo-de-funil",
            "utm_term": "ratingA+ratingB",
            "utm_content": "paginaA",
            "utm_id": "123456",
            "vv": 100,
            "cc": "BRL"
            }
        ]
    }

```
## Exemplo de carga
```typescript 
     // ...
      const response = await request.post(
        `/v2/?api_key=${api_key}&project_id=${project_id}&f=shorten`)
        .send({
            "links": [
                {
                "project_id": "agnostic-saas-01",
                "scope": "MY_KEY:MY_PROJECT_ID",
                "user_id": "123456",
                "is_active": true,
                "domain_short": "rslv.cc",
                "url_target": "mydomain-gigante.meusetor.minhaempresa.com.br",                
                "hash": "primeira",
                "redirect_to": "https://homolog.resolve.cenprot.org.br",
                "status": "created",
                "apsid": "pseudo---123456",
                "acid": "usuario-from-customer",
                "apid": "pixel-i781279123",
                "utm_source": "cenprot",
                "utm_medium": "email",
                "utm_campaign": "topo-de-funil",
                "utm_term": "ratingA+ratingB",
                "utm_content": "paginaA",
                "utm_id": "123456",
                "vv": 100,
                "cc": "BRL"
                }
            ]
            })
        .set('Content-Type', 'application/json')
        .set('Accept', 'application/json');
        // ....
```

# Pixel request (pixel_request)
Evento destinado a capturar abertura de páginas como e-mail ou mesmo HTMl. Para começar a receber eventos com  `pixel_request` adicione a uma tag `img` o atributo `src` para o Agnostic Pixel. 

```html

    <img src="https://utils.agnosticdata.ai/?
    ?f=pixel
    &acid=123456789
    &apid=123456789
    &cc=BRL&vv=100
    &api_key=123456789
    &project_id=123456789
    &utm_source=google
    &utm_medium=cpc
    &utm_campaign=googleads
    &utm_term=google
    &utm_content=google
    &utm_id=google
    &hash=plain or base64 or sha256 (default is base64)
    ">
```

Onde essas variáveis correspondem a: 
1. f: função pixel para receber apropriadamente a solicitação do pixel para cada usuário
1. acid: um código para identificar seu cliente unicamente
1. apid: agnostic pixel id, o código para identificar uma mensagem específica, um cliente pode ter n apid, desta forma, você pode compreender qual o tipo de campannha ou canal mais efetivo para cada cliente.
1. cc: representa a moeda para capturar o valor do evento. ex.: para enviar um email para o usuário foi R$ 0,33, logo cc será BRL (Default: BRL)
1. vv: representa o valor para capturar do evento. ex.: para enviar um email para o usuário foi R$ 0,33, logo vv decerá ser 33. 
1. api_key: chave do cliente Agnostic
1. project_id: projeto do cliente Agnostic
1. utm_*: variáveis de gestão de marketing
1. hash: define como você quer tratar os dados de contado do usuário, enviados dentro do payload event_data[1].type == complete. Caso, haja um objeto em `event_data` com um atributo `type` com o valor `complete` esses dados serão ofuscados (base64) ou anonymizados (sha256) ou armazenados como plain. 
  * observação: se vc utilizou pixellinks ou links para armezenar as URLS dos pixels ou dos redirects e fez tipo de uso de base64 ou sha256 lembre-se marcar cada pixel como `plain`, pois isso garante que o conteúdo não será ofuscado mais de uma vez, nem que assinatura do usuário com base em sha256 seja modificada. 
  * atenção: caso você não saiba o que isso quer dizer, lembre-se de nos perguntas, pois você pode perder as referências de assinatura dos usuários. 

  ## NOTAS
  NOTA 1: Se você utilizou a nossa api de **gerador de pixel** e ao subir dados de contato pessoal de cada cliente, desejou ofuscar já na base de pixels, OK! Agora os dados de contato do pixel, os `complete_data`, estão conforme a ofuscação enviada na requisição. Em seguida, quando o evento abertura de pixel ocorrer, ele vai levar o `complete_data` salvos na nossa api de pixel links e tentará anonimizar dados desse payload, caso não seja informado a variável `hash=plain`. Isso significa que você pode ter duas estratégias de anonimização, durante o POST para API Geradora de Pixel, ou na "Abertura do Pixel" passando por variável de URL. 

  NOTA 2: Se você utilizou a nossa api para gerar **redirect links (shorten)** não haverá uma segunda chave para passar o parâmetro de hash na URL, pois o modelo de URL do encurtador é `domain/hash` não cabendo espaço para uma variável. Desta forma, o event_data com `complete`, passado a um request de redirect, sempre irá considerar os dados como estão em `links` (da api geradora de links). Isso significa que sua estratégia de anonimização ocorre no `POST` para a API Redirect Links. 


# Complete data (complete_data)
Adicionar a lista `event_data` um objeto com o payloa de dados complementares como `event.event_data[{type: 'complete'}]`. Esse objeto adicional tem o atributo `type: complete` com dados do tipo complete, conforme abaixo:

Main options for has_hash are "plain", "false" , "base64", "sha256", but if has_hash is an string separated by comma, the first element will be consider the type of hash and the rest of elements will be the fields to hash.

    @example: has_hash: "sha256,firstname,lastname,email"
    @example: has_hash: "base64,firstname,lastname,email"


```typescript
    export interface ICompleteData { // ICDGeneralCase
    type?: Nullish<string> ; // "complete" is used to checks if event_data has type: complete
    save?: boolean; // if true save
    has_hash?: Nullish<string>; 
    email?: string; // em #ANZT
    phone?: string; // ph #ANZT
    firstname?: Nullish<string>; //fn #ANZT
    lastname?: Nullish<string>; //ln #ANZT
    date_born?: string; // db // date_born: "YYYY-MM-DD"
    gender?: string; // ge
    city?: string; //ct
    state?: string; // st
    zipcode?: string; // zp
    country?: string; // co
    order_id?: string; // oi //subscription_id
    // Integrations
    ps_id_ga?: string; // pseudo id dos caras google
    ps_id_fb?: string; // pseudo id facebook
    ps_id_uc?: string; // pseudo id uxcam
    ps_id_sg?: string; // pseudo id segment
    ps_id_hj?: string; // pseudo id hotjar
    ps_id_ap?: string; // pseudo id amplitude
    // App Store and Google Play
    install_id?: string; // application install hash id apple ou android
    }

```

## Utilizando o agnostica.identify()
Identify user for security reasons (into 1st party) and business purposes. Use on frontend. 

    * @param {string} user_id - user id
    * @param {object} complete_data - complete data of user

### Exemplo no navegador
```javascript
    adai.identify("user-hash-id-idenfier-uniq", {...complete_data});

    // complete_data
    const complete_data: ICompleteData = {
        email: "go@agnosticdata.ai", 
        phone: "61999931999",
    }
```

### Exemplo no backend (Complete Data): complete_data
```javascript
    /// Exemplo no backend
    // Passo 2: No backend, use sua melhor escolha para submeter um POST do evento passando encodeEvent
    //  
        const response = await fetch(TOKEN_URI); // token expira a cada uma 1 hora, solicitações em excesso no intervalo menor que 1h pode ser bloqueada.
        const {token, expires_in} = await response.json()
        const API_URL = `https://pubsub.googleapis.com/v1/projects/${AG_DB_CLOUD_PROJECT_ID}/topics/${AG_TOPIC_PRJID}:publish`;
        const response = await fetch(API_URL, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${token}`,
            "Content-Type": "application/json",
        },
        body: JSON.stringify({
        messages: [{ data: 
                Buffer.from(JSON.stringify({
                    created: Math.floor(Date.now() / 1000), // timestamp in seconds
                    event_name: "checkout_done",
                    scope: "MY_KEY:MY_PROJECT_ID",
                    app_info_version: "backend-v1",
                    action_source: "system_generated",
                    user_id: null, // user da transacao 
                    user_phone: null, // telefone de user se disponivel na transacao                    
                    items: [{id: "NR_CHAVE 2", quantity: 1, value: 20000, discount: 100}],
                    event_data: [
                        {   
                            content_name: "Payment Page 2", 
                            content_type: "Payment-Page-V2", 
                            value: 20450, 
                            currency: "BRL", 
                            tid: "Ad0CiCAM3uaM0R01", 
                            status: "payment_done", 
                            // coupon: null,
                            // shipping: null,
                            tax: 750
                        }, 
                        { // complete_data will be sent as an object. For all attributes see more in ICompleteData. 
                            type: "complete", 
                            has_hash: "plain", // sha256, base64, plain. Use plain for customer success and security reasons analytics. or sha256 for marketing purposes
                            email: "go@agnosticdata.ai", 
                            phone: "+55619999312199", 
                            firstname: "horacio"
                        }
                    ]
                })).toString("base64")
            }],        
        })
    });    
```

## Utilizando window.AG_ACID 
Utilize window.AG_ACID para associar um identificador de usuário (ID) ao pseudo_id e as querystring como apid (pixel id) ou utm. Desta forma, você pode compreender eventos do usuário que ocorreram antes mesmo dele se tornar um usuário da plataforma caso tenha já navegado no site. Esta é uma forma de associar eventos de usuário não autenticado (ou logado) a um usuário reconhecido do sistema.    


## Miscelânea

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

### FBClid
Você pode atribuir um fbclid (Facebook Pixel id a um evento) via querystring fbclid=IDFBCLID. Contudo lembre-se que Facebook é um *destination* e precisa ser configurado API_KEY e INSTANCE_ID nessas configurações. 

# Links
Para informações adicionais acesse:
* https://www.agnosticdata.ai/
* https://docs.agnosticads.com/
