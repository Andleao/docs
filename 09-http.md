----

<h2 id="http">*HTTP*</h2>

Nesta seção você ir&aacute; conhecer o processo de obtenção de dados via requisições HTTP.

----

<h3 id="request">HTTP Request</h3>

Para a obtenção de dados de requisições como **POST** e **GET** utiliza-se o objeto injetado *Request*.


As vantagens são muitas, dentre as principais pode-se listar a maior segurança, visto que os dados são tratados nativamente.


O objeto *Request* contém os seguintes métodos:

+ `setCustomFilters()`;
+ `get()`;
+ `post()`;
+ `getMethod()`;
+ `isPost()`;
+ `isGet()`;
+ `isPut()`, e;
+ `isHead()`.

O método `setCustomFilters()` tem o objetivo de customizar os filtros de tratamento aplicados aos dados das requisições. Para tal, é necessário informar um ***array* associativo** com o índice igual ao nome do campo e o valor com a constante de filtro. Leia: <a href="http://php.net/manual/en/filter.filters.sanitize.php" target="_blank">http://php.net/manual/en/filter.filters.sanitize.php</a>. Por padrão, o filtro aplicado em todos os dados é o `FILTER_SANITIZE_STRING` que evita a injeção de códigos HTML.


  O código resultante seria:
```php
  <?php
    class ProdutosController extends \HXPHP\System\Controller
    {

        public function salvarAction()
        {
            $this->request->setCustomFilters(array(
                'valor' => FILTER_SANITIZE_NUMBER_FLOAT
            ));

        }

    }
```


Já os métodos `get()` e `post()` retornam os dados filtrados, sendo que é possível retornar todo o conteúdo ou apenas um dado específico.


O código resultante seria:
```php
  <?php
    class ProdutosController extends \HXPHP\System\Controller
    {

        public function salvarAction()
        {
            $this->request->setCustomFilters(array(
                'valor' => FILTER_SANITIZE_NUMBER_FLOAT
            ));

            $this->request->post(); //Array com todos os dados enviados
            $this->request->post('valor'); //Apenas o conte&uacute;do do campo valor

        }

    }

```


E, por fim, tem-se os métodos: `getMethod()`, `isPost()`, `isGet()`, `isPut()` e `isHead()` que tem como função determinar qual é o método de requisição.