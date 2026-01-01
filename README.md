## Stubs
### O que são Stubs?
**Stubs são arquivos de template** que o Laravel usa como base para gerar novos arquivos quando você executa comandos do Artisan como `php artisan make:*`.

Tecnicamente, são arquivos `.stub` contendo código PHP com **placeholders** (marcadores) que são substituídos dinamicamente pelo Artisan.

##### Como funciona internamente?
Quando você roda, por exemplo:
```bash
php artisan make:controller UserController
```

O Laravel faz o seguinte:
1. **Localiza o stub** correspondente (neste caso, `controller.plain.stub`)
2. **Lê o conteúdo** do template
3. **Substitui os placeholders** pelos valores reais
4. **Cria o arquivo** no diretório correto

##### Exemplo de um stub original:
O stub de controller (`controller.plain.stub`) tem essa estrutura:
```php
<?php

namespace {{ namespace }};

use App\Http\Controllers\Controller;

class {{ class }} extends Controller
{
    //
}
```

Os placeholders `{{ namespace }}` e `{{ class }}` são substituídos pelo Artisan.

##### Onde ficam os stubs originais?
Ficam dentro do core do framework:
```
vendor/laravel/framework/src/Illuminate/Foundation/Console/stubs/
```

Lá você encontra stubs para tudo: models, migrations, seeders, controllers, middlewares, requests, etc.

#### Publicando os stubs
Quando você roda:
```bash
php artisan stub:publish
```

O Laravel **copia** todos os stubs para uma pasta `stubs/` na raiz do seu projeto:
```
seu-projeto/
├── app/
├── stubs/           ← pasta criada
│   ├── controller.plain.stub
│   ├── controller.stub
│   ├── migration.stub
│   ├── migration.create.stub
│   ├── model.stub
│   ├── seeder.stub
│   └── ... (vários outros)
├── ...
```

A partir daí, o Artisan **prioriza seus stubs customizados** sobre os originais do vendor. Isso te dá controle total sobre como o código gerado pelo Artisan é estruturado, incluindo o estilo de formatação das chaves.

> Os stubs desse projeto foram gerados no Laravel 12.30.1

#### Resumo técnico

|Aspecto|Descrição|
|---|---|
|**O que é**|Templates de código com placeholders|
|**Formato**|Arquivos `.stub` (texto puro)|
|**Localização original**|`vendor/laravel/framework/.../stubs/`|
|**Localização customizada**|`stubs/` na raiz do projeto|
|**Prioridade**|Stubs locais sobrescrevem os do vendor|
|**Placeholders comuns**|`{{ namespace }}`, `{{ class }}`, `{{ table }}`|

## Resumo do trabalho realizado:
### Conversão para padrão K&R
Mudei todas as chaves de abertura { para a mesma linha da declaração (classes, métodos, funções, etc.)

Resultado prático:
**PSR-12 / PER (padrão):**
```php
class User
{
    public function index()
    {
        //
    }
}
```

**K&R**
```php
class User {
    public function index() {
        //
    }
}
```

### Tradução dos comentários para português
Converti todos os comentários DocBlock de inglês para português, incluindo:
* "Create a new..." → "Cria uma nova..."
* "Display a listing..." → "Exibe uma listagem..."
* "Handle the event" → "Trata o evento"
* "Execute the job" → "Executa o job"
* E muitos outros

### Arquivos convertidos (52 arquivos no total)
* Enums (enum.stub, enum.backed.stub)
* Events (event.stub)
* Jobs (job.stub, job.queued.stub)
* Listeners (listener.stub, listener.queued.stub, listener.typed.stub, listener.typed.queued.stub)
* Mail (mail.stub, markdown-mail.stub)
* Notifications (notification.stub, markdown-notification.stub)
* Models (model.stub, model.pivot.stub)
* Observers (observer.stub, observer.plain.stub)
* Policies (policy.stub, policy.plain.stub)
* Providers (provider.stub)
* Requests (request.stub)
* Resources (resource.stub, resource-collection.stub)
* Rules (rule.stub)
* Scopes (scope.stub)
* Tests (test.stub, test.unit.stub, pest.stub, pest.unit.stub)
* Traits (trait.stub)
* View Components (view-component.stub)
* Factories (factory.stub)
* Seeders (seeder.stub)
* Migrations (migration.stub, migration.create.stub, migration.update.stub)
* Controllers (todos os 15 tipos de controllers)
* Middleware (middleware.stub)
* Console (console.stub)
* Classes (class.stub, class.invokable.stub)
* Casts (cast.stub, cast.inbound.stub)

Todos os stubs seguem o __padrão K&R__ com os __comentários em português__.