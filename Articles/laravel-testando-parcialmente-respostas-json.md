# Laravel: Testando Parcialmente Respostas JSON

> Este artigo é simplesmente uma tradução do artigo **[Testing Partial JSON Responses with Laravel][link-original-article]** escrito por **[Eric L. Barnes][link-original-author]** no blog **[Laravel News][link-laravel-news]**, com algumas pequenas alterações.

Laravel possui vários helpers para [testar][link-test-helpers] sua aplicação, incluindo até mesmo testes HTTP com uma API simples e fluente.

Uma das funcionalidades adicionadas na versão **5.4.10** é o método **assertJsonFragment**, ele permite que você procure por um fragmento específico dentro de uma resposta JSON.

Um exemplo rápido de como isso pode funcionar, vamos imaginar que a nossa aplicação precisa buscar um usuário específico:

``` php
Route::get('/api/users/{id}', function ($id) {
    return App\User::find($id);
});
```

Isso retorna um JSON com o usuário encontrado pelo **id** recebido via parametro na url:

``` json
{
    "id": 1,
    "name": "Anakin Skywalker",
    "email": "anakin@death.star",
    "created_at": "2017-02-14 01:53:04",
    "updated_at": "2017-02-14 01:53:04"
}
```

Podemos testar isso usando o `assertJsonFragment` da seguinte forma:

``` php
public function testPartialJsonResponse()
{
    $response = $this->json('GET', '/api/users/1');

    $response
        ->assertStatus(200)
        ->assertJsonFragment([
            'name' => 'Anakin Skywalker',
        ]);
}
```

Isso é apenas uma das várias ferramentas disponíveis que facilitam escrever testes no Laravel. De uma olhada na [documentação][link-documentation] para ver outros métodos que ajudam a testar respostas JSON.

[link-test-helpers]: https://laravel-news.com/tag/testing
[link-documentation]: https://laravel.com/docs/5.4/http-tests#testing-json-apis
[link-original-article]: https://laravel-news.com/testing-partial-json
[link-original-author]: https://laravel-news.com/@ericlbarnes
[link-laravel-news]: https://laravel-news.com
