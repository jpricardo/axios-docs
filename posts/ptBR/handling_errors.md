---
title: 'Lidando com Erros'
prev_title: 'Interceptadores'
prev_link: '/ptBR/docs/interceptors'
next_title: 'Cancelamento'
next_link: '/ptBR/docs/cancellation'
---

```js
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // A requisição foi feita e o servidor respondeu com um código de status
      // que cai fora do intervalo 200 a 299
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // A requisição foi feita mas nenhuma resposta foi recebida
      // `error.request` é uma instância do XMLHttpRequest no navegador e uma instância de
      // http.ClientRequest no node.js
      console.log(error.request);
    } else {
      // Alguma coisa acontenceu ao configurar a requisição, gerando um erro.
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```

Usando a configuração opcional `validateStatus`, você pode definir o(s) código(s) HTTP que devem lançar um erro.

```js
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // Resolve somente se o código de status for menor que 500
  }
})
```

Usando o `toJSON` você pode receber um objeto com mais informações sobre o erro HTTP.

```js
axios.get('/user/12345')
  .catch(function (error) {
    console.log(error.toJSON());
  });
```