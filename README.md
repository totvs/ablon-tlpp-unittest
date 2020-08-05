# Ablon

Simplest and Lightest unit test framework for TLPP.

## Como buildar

Compilar a pasta src inteira no repo

## Como usar
Adicionar a pasta \annotations no seu include path ( Conforme a extensão utilizada)

simple.spec.tlpp
 ```
#include "test.th"
@test("Eu sou outro Teste, eu estou correto")
function mytlpptest2()
    Assert():AreEqual(3,3)
return

 ```