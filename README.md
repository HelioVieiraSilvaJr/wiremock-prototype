# Prototipo para fazer Mock's usando o wiremock.

Para rodar no Mac ou Linux:

`java -jar wiremock-jre8-standalone-2.26.3.jar --port 80 --verbose`

Para rodar no Windows:

`double click in batch file run-windows.bat`

Baixar Java

`https://www.java.com/pt-BR/download/manual.jsp`

Documentação oficial:

`http://wiremock.org/docs/getting-started/`


## Recursos mais comuns

Verificar se o Body possui chaves parametros específicos
```
"request": {
  "bodyPatterns": [
    { "matchesJsonPath": "$.id" },
    { "matchesJsonPath": "$.name" }
    { "matchesJsonPath": "$.message" }
  ]
}
```

Verificar se o Body possui chaves de parametros específicos aplicando Regex
```
"request": {
  "bodyPatterns": [
    { "matchesJsonPath" : "$[?(@.cpf =~ /[0-9]{11}/i)]" }
    { "matchesJsonPath" : "$[?(@.cnpj =~ /[0-9]{14}/i)]" }
  ]
}
```

Verificar se o Body possui chaves e valores específicos
```
"request": {
  "bodyPatterns": [
    {
      "equalToJson": "{\"password\":\"1234\",\"email\":\"joao@email.com\"}",
      "ignoreArrayOrder": true,
      "ignoreExtraElements": true
    }
  ]
}
```

Verifica de o Header possui chaves e valores específicos
```
"request": {
  "headers": {
    "user-token": {
      "contains": "TOKEN-DO-USUARIO"
    }
  }
}
```

Para ter mais de um Stub de teste para o mesmo contexto, deve-se adiciona-los no array da estrutura abaixo
```
{
  "mappings": []
}
```

Quando temos varios Stubs que se sobrepõem, podemos estabelecer uma prioridade para cada Stub usando `"priority"`
```
{
  "priority": 1
}
```

Para adicionar um tempo de resposta, basta usar a chave `"fixedDelayMilliseconds"`
```
"response" : {
  "fixedDelayMilliseconds": 3000
}
```

Temos 2 principais maneiras de responder ao request:

- Apontar para um arquivo com o Payload definido usando a chave `"bodyFileName"`
```
"response" : {
  "bodyFileName" : "validations/document.json",
}
```
- Ou escrever o Payload usando a chave `"body"`
```
"response" : {
  "body": "{ \"status\":\"invalid_document\", \"message\":\"Os números não correspondem ao CPF cadastrado. \\n Tente novamente.\"}"
}
```