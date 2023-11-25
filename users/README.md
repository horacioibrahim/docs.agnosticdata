# Documentação do SDK Agnostic Data Web v1.0.1
Este SDK fornece uma série de funções e variáveis que permitem aos desenvolvedores web implementar recursos específicos em suas aplicações.

## Variáveis auto-preenchidas (não modificar)
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

## Meta-tags
* **agnostic_inactivate_minutes**: Esta meta-tag pode ser usada para definir uma duração de sessão personalizada. O valor deve ser fornecido em minutos. Se o valor fornecido não for um número, a duração da sessão será definida como o valor padrão de 5 minutos.
```html
<meta name="agnostic_inactivate_minutes" content="10">
```

## Elementos com Prefixo "agnostic_" para tracking click com contexto
Seleciona todos os elementos cujo id ou class começa com "agnostic_". Você pode usar a tag para elementos com o prefixo "agnostic_". 

Vamos supor que você quer identificar um botão em seu site que tem um papel importante, como um botão de compra. O exemplo abaixo, envia automaticamente dentro do evento de click o atributo `postfix_text` com "purchaseButton". 
```html
<button id="agnostic_purchaseButton">Comprar Agora</button>
```
ou se tiver utilizando class onde no exemplo abaixo, automaticamente enviará dentro do evento de click o atributo `postfix_text` com "specialOffer". 
```html
<button class="agnostic_specialOffer">Oferta Especial</button>
``````
## Rastreamento de Cliques 
Defina uma lista de seletores para rastreamento de cliques, incluindo botões, links, elementos com id/class prefixados com "agnostic_", e vários tipos de campos de entrada. Abaixo os valores padrões dos elementos que serão capturados os clicks. Modifique essa lista se quiser controlar os elementos que enviam evento de clique. 

**Importante**: redefinir o comporamento padrão pode impactar na captura de eventos prefixados com `agnostic_`

```html
<meta name="agnostic_click_listeners" content='button, a, [id^="agnostic_"], [class^="agnostic_"], input, select, textarea, checkbox, radio, image, img, tab'>
```

## Variáveis de Meta Tag para Análise de Conteúdo (automático)
Essas variáveis permitem uma análise detalhada e personalizada do conteúdo da página, ajudando na tomada de decisões baseadas em dados e na personalização de experiências de usuário. Quando configuradas são capturadas automaticamente sem a necessidade de criar um objeto específico de evento. (veja eventos específicos mais abaixo)

1. Tipo de Conteúdo (agnostic_content_type)
    
    * **Descrição**: Define o tipo de conteúdo da página (ex: artigo, produto, categoria, teste A/B).
    * **Valor**: Pode ser uma string fixa (ex: "article") ou dinamicamente gerada pelo código baseada no conteúdo da página.
    ```html
    <!-- Exemplo para agnostic_content_type -->
    <meta name="agnostic_content_type" content="article">
    <!-- Exemplo de uso: Esta meta tag define o tipo de conteúdo da página, por exemplo, um artigo -->
    ```
2. Categoria de Conteúdo (agnostic_content_category)
    
    **Descrição**: Especifica a categoria do conteúdo (ex: notícias, esportes, moda, elétrica, hidráulca, protestos, emolumentos).
    **Valor**: Pode ser uma string fixa (ex: "news") ou gerada dinamicamente para refletir a categoria do conteúdo da página.
    ```html
    <!-- Exemplo para agnostic_content_category -->
    <meta name="agnostic_content_category" content="news">
    <!-- Exemplo de uso: Esta meta tag define a categoria de conteúdo da página, como notícias -->
    ```    
3. ID do Item (agnostic_item_id)
    
    * **Descrição**: Define um identificador único para o item na página, como o ID de um produto ou artigo.
    * **Valor**: Normalmente gerado dinamicamente para corresponder ao ID específico do item sendo exibido.
    ```html
    <!-- Exemplo para agnostic_item_id -->
    <meta name="agnostic_item_id" content="12345">
    <!-- Exemplo de uso: Esta meta tag define um ID único para o item na página, como o ID de um produto ou artigo -->
    ```   
4. Nome do Item (agnostic_item_name)
    
    * **Descrição**: Define o nome do item na página, como o nome de um produto ou o título de um artigo.
    * **Valor**: Geralmente gerado dinamicamente para refletir o nome real do item em questão.
    ```html
    <!-- Exemplo para agnostic_item_name -->
    <meta name="agnostic_item_name" content="Nome do Produto">
    <!-- Exemplo de uso: Esta meta tag define o nome do item na página, como o nome de um produto ou o título de um artigo -->    
    ```    
5. Promoção (agnostic_is_promo)
    
    * **Descrição**: Indica se o conteúdo é promocional.
    * **Valor**: Pode ser uma string fixa ("true" ou "false") ou determinada dinamicamente com base na natureza do conteúdo.
    ```html
    <!-- Exemplo para agnostic_is_promo -->
    <meta name="agnostic_is_promo" content="true">
    <!-- Exemplo de uso: Esta meta tag define se o conteúdo é promocional -->    
    ```    
6. ID da Promoção (agnostic_promotion_id)
    
    * **Descrição**: Define o ID de uma promoção para campanhas de marketing.
    * **Valor**: Pode ser uma string fixa ou gerada dinamicamente para corresponder à promoção específica.
    ```html
    <!-- Exemplo para agnostic_promotion_id -->
    <meta name="agnostic_promotion_id" content="promo123">
    <!-- Exemplo de uso: Esta meta tag define o ID de uma promoção para campanhas de marketing -->    
    ```    
7. Nome da Promoção (agnostic_promotion_name)
    
    * **Descrição**: Define o nome de uma promoção para campanhas de marketing.
    * **Valor**: Pode ser uma string fixa ou gerada dinamicamente para corresponder ao nome da promoção.
    ```html
    <!-- Exemplo para agnostic_promotion_name -->
    <meta name="agnostic_promotion_name" content="Promoção de Verão">
    <!-- Exemplo de uso: Esta meta tag define o nome de uma promoção para campanhas de marketing -->    
    ```    
8. Moeda (agnostic_currency)
    
    * **Descrição**: Define a moeda usada para quaisquer valores monetários na página.
    * **Valor**: Geralmente uma string fixa representando o código da moeda (ex: "USD", "EUR", "BRL").
    ```html
    <!-- Exemplo para agnostic_currency -->
    <meta name="agnostic_currency" content="BRL">
    <!-- Exemplo de uso: Esta meta tag define a moeda usada para valores na página -->
    ```    
9. Valor (agnostic_value)
    
    * **Descrição**: Define o valor monetário associado ao conteúdo, como o preço de um produto.
    * **Valor**: Pode ser fixo ou dinamicamente gerado, especialmente útil para páginas de produtos onde o preço pode variar.
    ```html
    <!-- Exemplo para agnostic_value -->
    <meta name="agnostic_value" content="199.99">
    <!-- Exemplo de uso: Esta meta tag define o valor do conteúdo, como o preço de um produto ou o custo de um artigo -->    
    ```    

# window.agnostica()
A função window.agnostica é utilizada para enviar eventos para o sistema Agnostica é composta de 3 variáveis: nome do evento, dados contextuais e campos específicos do evento.

```javascript
// Recebe o nome do evento, contextFields e specificFields e envia o fluxo onde:
// contextFields: user_id, user_pseudo_id, user_phone, userToken, is_promo, items
// specificFields: campos específicos do evento com validação. Veja a documentação. Ex.: {product_id: 123, product_name: "produto 1"}

let contextFields = {}
let specificFields = {}
window.agnostica("event_name", contextFields, specificFields)
```

Aqui está um exemplo de evento que podem ser enviados usando esta função. Contudo, este evento é enviado automaticamente quando o usuário clica em um elemento na interface do usuário. Hipoteticamente, pode ser enviado manualmente com:
```javascript
window.agnostica('click', contextFields, complement);
```
* `contextFields`: Este objeto contém informações contextuais sobre o evento, como o ID do usuário (veja em "ContextFields Enriquecendo as varáveis de contexto")
* `complement`: Este objeto contém informações adicionais sobre o evento, como o ID do elemento clicado, o texto do elemento clicado, etc. (veja documentação)

## contextFields
Os `contextFields` dão contexto ao evento e compõe o payload. 
```javascript
    let event = {
        ...contextFields,
        event_data: [{ ...specificFields }],
    };
```

## ContextFields Enriquecendo as varáveis de contexto
Você pode enriquecer as variáveis de contexto. IMPORTANTE: não altere a variável **scope** e nenhuma das variáveis em **## Variáveis auto-preenchidas (não modificar)**,
pois a solução poderá parar de capturar e o projeto ser bloqueado automaticamente. Abaixo descrevemos essas variáveis que podem ser enriquecidas quando na WEB, dado a necessidade. 

Seguem exemplos de uso dos campos de contexto (contextFields) que você poderá alterar e escolher valores (quando na WEB):

- `event_provider?: Nullable<string>`(@future indisponivel no momento)
    * **Descrição:** O fornecedor do evento para o marketplace futuro, caso seja um evento criado por outros provedores 
    * **Tipo:** String ou `null`.

- `app_info_version: string`
    * **Descrição:** A versão do app ou site. 
    * **Exemplo:** "tom-4.0.1" ou "web-4.0.1" ou "presto-4.0.1".

- `app_package_name: Nullable<string>`
    * **Descrição:** Nome do pacote ou site.     
    * **Tipo:** String ou `null`.
    * **Exemplo:** "com.agnosticdata.app" ou URL.
    * **Comportamento**: quando na web irá automaticamente capturar `window.location.hostname` (url do site sem caminhos relativos); quando não informado irá buscar a definição padrão realizada na Console => Project => Settings. 

- `relative_view?: Nullable<string>`  
    * **Descrição:** Usado para conter page_view e screen_view relativa 
    * **Tipo:** String ou `null`.
    * **Exemplo:** "domain.com/relativeURL/relativeAgain" ou "com.lovyca.app.relativeURL".
    * **Comportamento**: na web é automaticamente capturada por `window.location.pathname` (caminho relativo do site). Em mobile a cada view carregada chame o evento (ex.: onRender)

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


### Estrutura de um Item
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

## SpecificFields: Eventos
Os campos específicos são campos contidos especificamene em cada evento. Eles são validados durante o processamento, logo cada evento chamado em agnostic("event_name", ... ,  specificFields) tem sua própria estrutura e comporamento. Para saber mais sobre o conteúdo dos eventos acesso a console e navegue no catálogo. 


## Miscelânea

### FBClid
Você pode atribuir um fbclid (Facebook Pixel id a um evento) via querystring fbclid=IDFBCLID. Contudo lembre-se que Facebook é um *destination* e precisa ser configurado API_KEY e INSTANCE_ID nessas configurações. 
