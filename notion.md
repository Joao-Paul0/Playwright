### Cite exemplo de um código .js usando playwright pegando seletores/elementos

Aqui está um exemplo de código JavaScript utilizando o Playwright para acessar elementos em uma página web por meio de seletores:

```js
const { chromium } = require("playwright");

(async () => {
  const browser = await chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();

  await page.goto("https://www.example.com");

  // Exemplo de seleção de elementos por seletor CSS
  const titleElement = await page.$("h1");
  const titleText = await titleElement.innerText();
  console.log("Título:", titleText);

  // Exemplo de seleção de elementos por XPath
  const linkElement = await page.$x("//a[contains(text(), 'Saiba mais')]");
  const linkHref = await linkElement[0].getAttribute("href");
  console.log("Link:", linkHref);

  await browser.close();
})();
```

Neste exemplo, o código utiliza o Playwright para abrir uma página web, no caso o "https://www.example.com". Em seguida, são realizadas duas seleções de elementos, uma usando um seletor CSS e outra utilizando XPath.
<br>

1. O seletor CSS h1 é utilizado para selecionar o elemento `<h1>` na página, que normalmente representa o título principal. Em seguida, o método innerText() é utilizado para obter o texto contido no elemento selecionado.
   <br>
2. O XPath //a[contains(text(), 'Saiba mais')] é utilizado para selecionar um link contendo o texto "Saiba mais". A função $x() retorna uma lista de elementos correspondentes ao XPath fornecido. Nesse caso, é selecionado o primeiro elemento da lista (índice [0]). Em seguida, o método getAttribute('href') é utilizado para obter o valor do atributo "href" do link selecionado.
   <br>
   <br>
   Após a execução, o código imprime o título e o link obtidos a partir dos elementos selecionados.
   <br>
   <br>
   Lembre-se de ajustar os seletores CSS e XPath de acordo com a estrutura da página que você está testando.

### Melhore o código acima usando uma opção melhor disponível para a localização de elementos específicos.

Aprimorando o código anterior para utilizar uma opção melhor disponível para a localização dos elementos específicos, utilizando seletores CSS mais estáveis.

```js
const { chromium } = require("playwright");

(async () => {
  const browser = await chromium.launch();
  const context = await browser.newContext();
  const page = await context.newPage();

  await page.goto("https://www.example.com");

  // Seleção do elemento por um seletor CSS mais estável
  const titleElement = await page.$("h1#main-title");
  const titleText = await titleElement.innerText();
  console.log("Título:", titleText);

  // Seleção do link por um seletor CSS mais específico
  const linkElement = await page.$("a.learn-more-link");
  const linkHref = await linkElement.getAttribute("href");
  console.log("Link:", linkHref);

  await browser.close();
})();
```

Neste código aprimorado, utilizei seletores CSS mais específicos para localizar os elementos desejados.

1. No exemplo do título, utilizei o seletor CSS 'h1#main-title'. Aqui, estamos selecionando o elemento `<h1>` com o atributo id "main-title", que provavelmente é mais estável e exclusivo para o título principal da página.
2. No exemplo do link "Saiba mais", utilizei o seletor CSS 'a.learn-more-link'. Neste caso, estamos selecionando o elemento `<a>` com a classe "learn-more-link". Essa classe específica pode ser mais estável do que apenas buscar o texto "Saiba mais" no link, uma vez que o texto pode ser alterado, mas a classe é mais provável de se manter constante.
   <br>
   <br>
   Ao utilizar seletores CSS mais específicos e estáveis, podemos evitar dependências excessivas de XPath e tornar os testes de automação mais robustos às mudanças na estrutura da página.
   <br>
   <br>
   Lembre-se de ajustar os seletores CSS de acordo com a estrutura da página que você está testando.
