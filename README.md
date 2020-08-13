# Ablon

Simplest and Lightest unit test framework for TLPP.

## Como buildar

Compilar a pasta src inteira no repo


# Como usar
## Configure seu IDE
    Adicionar a pasta \annotations no seu include path ( Conforme a extensão utilizada)
## Use boas praticas
    Essa lib de test recomenda o uso do padrão (NOMEDOFONTE.spec.tlpp ) aonde o nome do fonte, é fonte que esta em tlpp

## Exemplos    
simple.spec.tlpp
 ```
#include "test.th"
@test("Eu sou outro Teste, eu estou correto")
function mytlpptest2()
    Assert():AreEqual(3,3)
return

 ```

## Testando Rests
Utilizando o rest do [TLPP](https://tdn.totvs.com/display/tec/Rest)

myservice.tlpp
 ```
#include "test.th"

#include "tlpp-core.th"
namespace sample.customer
using namespace sample.customer.util

@post("/api/sample/customer/")
function post()
    local cBody := oRest:getBodyRequest()
    local jBody
    local cErrorParser
    local oService := CustomerService():getInstance()    
    if (empty(cBody))
        oRest:setFault("Body invalid")
        oRest:setStatusCode(403)
    else    
        jBody := JsonObject():new()
        cErrorParser := jBody:fromJson(cBody)
        if (empty(cErrorParser))
            oService:Insert(jBody)
        else
            oRest:setFault("Body invalid")
            oRest:setStatusCode(403)
        endif
    endif

return


 ```

myservice.spec.tlpp
 ```
#include "test.th"

using namespace tunittest.core
using namespace tunittest.assistant
using namespace sample.customer

@test("testa Post em branco, espero que retorne erro")
function postCustomertest01()
    //Mockando alguem enviando o request
    
    TlppRestMock():createPostRequest()
    //Chamo o servico
    post()
    Assert():AreEqual(oRest:getStatusCode(),403,"Body errado")    
return
 ```
# Rodando seus testes
## Utilizando extesão do Vscode 
A extensão [Ablon an Unit Test for TLPP and Advpl](https://marketplace.visualstudio.com/items?itemName=KillerAll.advpl-unit-test) , está disponivel para que utiliza a extensão [I Love Advpl](https://marketplace.visualstudio.com/items?itemName=KillerAll.advpl-vscode)
Ainda não é conhecido suporte pela extensão TDS.

## Para rodar manualmente 
```
tunittest.main.u_executeTestByFile("test-simple.spec.tlpp")
```

## Debug do teste

Chamar no launch do debug a função:
```
 tunittest.main.u_testDebug(cFileName as character,cFunctionName as character)
```

 