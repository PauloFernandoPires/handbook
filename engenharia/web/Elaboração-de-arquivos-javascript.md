O uso de javascript na solução aconteceu sempre de forma evolutiva dentro da equipe. Em uma das última rodadas para estabelecer um padrão de escrita, as seguintes diretrizes foram estabelecidas

- Evitar **ao máximo** escrever código javascript nas páginas cshtml. Javascript deve ser escrito em arquivos js.
- Incluir javascripts no final da página, antes da tag \</body>\.

# Passagem de parâmetros entre Razor e arquivos javascript
Pode existir a necessidade de se passar parâmetros que vieram do servidor para o javascript. A melhor forma de realizar é usando o atributo [data-*](https://www.w3schools.com/tags/att_data-.asp) em tags HTML.

Exemplo:
No HTML, adicionar o campo data-* em qualquer tag desejada (aqui, em um campo hidden)
```html
  <input type="hidden" id="campoContainerID" data-containerID="2">
```

No Javascript, usar Jquery para capturar esse campo.
```js
  var containerID = $("#campoContainerID").data("containerID")
```

A solução antiga era criar um bloco script que carregava as variáveis de servidor em um objeto e depois chamava um método 'init' passando esses parâmetros. A vantagem dessa solução é que não é necessário escrever código algum de javascript no cshtml.