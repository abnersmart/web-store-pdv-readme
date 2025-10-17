# Guia Rápido: Sintaxe Delphi para quem já programa

## 1. Variáveis e Tipos

### Python
```python
nome = "João"
idade = 25
altura = 1.75
ativo = True
```

### C#
```csharp
string nome = "João";
int idade = 25;
double altura = 1.75;
bool ativo = true;
```

### Delphi
```pascal
var
  nome: string;
  idade: Integer;
  altura: Double;
  ativo: Boolean;
begin
  nome := 'João';    // Aspas simples!
  idade := 25;       // := para atribuição
  altura := 1.75;
  ativo := True;     // True com T maiúsculo
end;
```

---

## 2. Estruturas de Controle

### If/Else

**Python:**
```python
if idade >= 18:
    print("Maior de idade")
else:
    print("Menor de idade")
```

**C#:**
```csharp
if (idade >= 18)
{
    Console.WriteLine("Maior de idade");
}
else
{
    Console.WriteLine("Menor de idade");
}
```

**Delphi:**
```pascal
if idade >= 18 then
  Writeln('Maior de idade')
else
  Writeln('Menor de idade');

// Se tiver mais de uma linha, use begin/end:
if idade >= 18 then
begin
  Writeln('Maior de idade');
  Writeln('Bem-vindo!');
end;
```

---

### For Loop

**Python:**
```python
for i in range(10):
    print(i)

for item in lista:
    print(item)
```

**C#:**
```csharp
for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}

foreach (var item in lista)
{
    Console.WriteLine(item);
}
```

**Delphi:**
```pascal
var
  i: Integer;
  item: string;
  lista: TStringList;
begin
  // Loop tradicional
  for i := 0 to 9 do
    Writeln(i);
  
  // Loop reverso
  for i := 9 downto 0 do
    Writeln(i);
  
  // For-in (Delphi moderno)
  lista := TStringList.Create;
  try
    for item in lista do
      Writeln(item);
  finally
    lista.Free;
  end;
end;
```

---

### While Loop

**Python:**
```python
contador = 0
while contador < 10:
    print(contador)
    contador += 1
```

**C#:**
```csharp
int contador = 0;
while (contador < 10)
{
    Console.WriteLine(contador);
    contador++;
}
```

**Delphi:**
```pascal
var
  contador: Integer;
begin
  contador := 0;
  while contador < 10 do
  begin
    Writeln(contador);
    Inc(contador);  // Inc() = contador := contador + 1
  end;
end;
```

---

## 3. Funções e Procedures

### Python
```python
def somar(a, b):
    return a + b

def imprimir_mensagem(texto):
    print(texto)

resultado = somar(5, 3)
```

### C#
```csharp
int Somar(int a, int b)
{
    return a + b;
}

void ImprimirMensagem(string texto)
{
    Console.WriteLine(texto);
}

int resultado = Somar(5, 3);
```

### Delphi
```pascal
// Function = retorna valor
function Somar(a, b: Integer): Integer;
begin
  Result := a + b;  // Result é a variável de retorno
end;

// Procedure = não retorna valor (void)
procedure ImprimirMensagem(texto: string);
begin
  Writeln(texto);
end;

var
  resultado: Integer;
begin
  resultado := Somar(5, 3);
  ImprimirMensagem('Olá');
end;
```

---

## 4. Classes e Objetos

### Python
```python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade
    
    def apresentar(self):
        return f"Olá, sou {self.nome}"

pessoa = Pessoa("João", 25)
print(pessoa.apresentar())
```

### C#
```csharp
public class Pessoa
{
    private string nome;
    private int idade;
    
    public Pessoa(string nome, int idade)
    {
        this.nome = nome;
        this.idade = idade;
    }
    
    public string Apresentar()
    {
        return $"Olá, sou {nome}";
    }
}

Pessoa pessoa = new Pessoa("João", 25);
Console.WriteLine(pessoa.Apresentar());
```

### Delphi
```pascal
type
  TPessoa = class
  private
    FNome: string;      // F = Field (convenção)
    FIdade: Integer;
  public
    constructor Create(ANome: string; AIdade: Integer);
    destructor Destroy; override;
    function Apresentar: string;
    
    property Nome: string read FNome write FNome;   // Property = getter/setter
    property Idade: Integer read FIdade write FIdade;
  end;

implementation

constructor TPessoa.Create(ANome: string; AIdade: Integer);
begin
  inherited Create;  // Chama construtor da classe pai
  FNome := ANome;
  FIdade := AIdade;
end;

destructor TPessoa.Destroy;
begin
  // Limpeza de recursos
  inherited Destroy;
end;

function TPessoa.Apresentar: string;
begin
  Result := 'Olá, sou ' + FNome;
end;

// Usando a classe:
var
  pessoa: TPessoa;
begin
  pessoa := TPessoa.Create('João', 25);
  try
    Writeln(pessoa.Apresentar);
    Writeln(pessoa.Nome);  // Usa property
  finally
    pessoa.Free;  // IMPORTANTE: sempre liberar memória!
  end;
end;
```

---

## 5. Trabalhando com JSON

### Python
```python
import json

# Criar JSON
dados = {
    "nome": "João",
    "idade": 25,
    "ativo": True
}
json_string = json.dumps(dados)

# Parse JSON
dados_parse = json.loads(json_string)
print(dados_parse["nome"])
```

### C#
```csharp
using Newtonsoft.Json;

// Criar JSON
var dados = new {
    nome = "João",
    idade = 25,
    ativo = true
};
string jsonString = JsonConvert.SerializeObject(dados);

// Parse JSON
var dadosParse = JsonConvert.DeserializeObject<dynamic>(jsonString);
Console.WriteLine(dadosParse.nome);
```

### Delphi
```pascal
uses System.JSON;

var
  LJson: TJSONObject;
  LJsonString: string;
begin
  // Criar JSON
  LJson := TJSONObject.Create;
  try
    LJson.AddPair('nome', 'João');
    LJson.AddPair('idade', TJSONNumber.Create(25));
    LJson.AddPair('ativo', TJSONBool.Create(True));
    
    LJsonString := LJson.ToString;
    Writeln(LJsonString);
  finally
    LJson.Free;
  end;
  
  // Parse JSON
  LJson := TJSONObject.ParseJSONValue(LJsonString) as TJSONObject;
  try
    Writeln(LJson.GetValue<string>('nome'));
    Writeln(LJson.GetValue<Integer>('idade'));
    Writeln(LJson.GetValue<Boolean>('ativo'));
  finally
    LJson.Free;
  end;
end;
```

---

## 6. Requisições HTTP

### Python
```python
import requests

# GET
response = requests.get('https://api.example.com/data')
print(response.json())

# POST
data = {"key": "value"}
response = requests.post('https://api.example.com/data', json=data)
print(response.status_code)
```

### C#
```csharp
using System.Net.Http;

var client = new HttpClient();

// GET
var response = await client.GetAsync("https://api.example.com/data");
var content = await response.Content.ReadAsStringAsync();

// POST
var data = new { key = "value" };
var json = JsonConvert.SerializeObject(data);
var content = new StringContent(json, Encoding.UTF8, "application/json");
var response = await client.PostAsync("https://api.example.com/data", content);
```

### Delphi
```pascal
uses RESTRequest4D;

var
  LResponse: IResponse;
begin
  // GET
  LResponse := TRequest.New
    .BaseURL('https://api.example.com/data')
    .Accept('application/json')
    .Get;
  
  Writeln(LResponse.Content);
  
  // POST
  LResponse := TRequest.New
    .BaseURL('https://api.example.com/data')
    .AddBody('{"key":"value"}')
    .ContentType('application/json')
    .Post;
  
  Writeln(LResponse.StatusCode);
end;
```

---

## 7. Exceções (Try/Catch)

### Python
```python
try:
    resultado = 10 / 0
except ZeroDivisionError as e:
    print(f"Erro: {e}")
except Exception as e:
    print(f"Erro geral: {e}")
finally:
    print("Sempre executa")
```

### C#
```csharp
try
{
    int resultado = 10 / 0;
}
catch (DivideByZeroException ex)
{
    Console.WriteLine($"Erro: {ex.Message}");
}
catch (Exception ex)
{
    Console.WriteLine($"Erro geral: {ex.Message}");
}
finally
{
    Console.WriteLine("Sempre executa");
}
```

### Delphi
```pascal
try
  resultado := 10 div 0;  // div = divisão inteira
except
  on E: EDivByZero do
    Writeln('Erro: ' + E.Message);
  on E: Exception do
    Writeln('Erro geral: ' + E.Message);
end;

// Try/Finally (não captura exceção, só executa limpeza)
LJson := TJSONObject.Create;
try
  // Usa LJson
finally
  LJson.Free;  // SEMPRE executa, mesmo com exceção
end;
```

---

## 8. Listas/Arrays

### Python
```python
# Lista
lista = ["a", "b", "c"]
lista.append("d")
print(len(lista))

for item in lista:
    print(item)
```

### C#
```csharp
// Lista
var lista = new List<string> { "a", "b", "c" };
lista.Add("d");
Console.WriteLine(lista.Count);

foreach (var item in lista)
{
    Console.WriteLine(item);
}
```

### Delphi
```pascal
uses System.Generics.Collections;

var
  lista: TList<string>;
  item: string;
begin
  lista := TList<string>.Create;
  try
    lista.Add('a');
    lista.Add('b');
    lista.Add('c');
    lista.Add('d');
    
    Writeln('Total: ', lista.Count);
    
    // For tradicional
    for var i := 0 to lista.Count - 1 do
      Writeln(lista[i]);
    
    // For-in
    for item in lista do
      Writeln(item);
      
  finally
    lista.Free;
  end;
end;

// Ou use TStringList para strings:
var
  lista: TStringList;
begin
  lista := TStringList.Create;
  try
    lista.Add('a');
    lista.Add('b');
    Writeln(lista.Count);
  finally
    lista.Free;
  end;
end;
```

---

## 9. Dicionários/Hash Maps

### Python
```python
dicio = {
    "nome": "João",
    "idade": 25
}
print(dicio["nome"])
dicio["cidade"] = "São Paulo"
```

### C#
```csharp
var dicio = new Dictionary<string, object>
{
    {"nome", "João"},
    {"idade", 25}
};
Console.WriteLine(dicio["nome"]);
dicio["cidade"] = "São Paulo";
```

### Delphi
```pascal
uses System.Generics.Collections;

var
  dicio: TDictionary<string, string>;
begin
  dicio := TDictionary<string, string>.Create;
  try
    dicio.Add('nome', 'João');
    dicio.Add('idade', '25');
    
    Writeln(dicio['nome']);
    
    dicio.AddOrSetValue('cidade', 'São Paulo');
    
    // Verificar se existe
    if dicio.ContainsKey('nome') then
      Writeln('Nome existe!');
      
  finally
    dicio.Free;
  end;
end;
```

---

## 10. Strings

### Python
```python
texto = "Olá Mundo"
print(texto.upper())
print(texto.lower())
print(texto.replace("Mundo", "Python"))
print(f"Nome: {nome}, Idade: {idade}")  # f-string
```

### C#
```csharp
string texto = "Olá Mundo";
Console.WriteLine(texto.ToUpper());
Console.WriteLine(texto.ToLower());
Console.WriteLine(texto.Replace("Mundo", "C#"));
Console.WriteLine($"Nome: {nome}, Idade: {idade}");  // interpolação
```

### Delphi
```pascal
var
  texto: string;
begin
  texto := 'Olá Mundo';
  Writeln(UpperCase(texto));
  Writeln(LowerCase(texto));
  Writeln(StringReplace(texto, 'Mundo', 'Delphi', [rfReplaceAll]));
  Writeln(Format('Nome: %s, Idade: %d', [nome, idade]));  // Format
  
  // Concatenação
  texto := 'Olá' + ' ' + 'Mundo';
  
  // Substring (1-based index!)
  Writeln(Copy(texto, 1, 3));  // 'Olá' (índice começa em 1!)
  
  // Length
  Writeln(Length(texto));
end;
```

---

## 11. Conversões de Tipo

### Python
```python
numero = int("123")
texto = str(123)
real = float("3.14")
```

### C#
```csharp
int numero = int.Parse("123");
string texto = 123.ToString();
double real = double.Parse("3.14");
```

### Delphi
```pascal
var
  numero: Integer;
  texto: string;
  real: Double;
begin
  numero := StrToInt('123');
  texto := IntToStr(123);
  real := StrToFloat('3.14');
  
  // Conversões seguras (retorna default se falhar)
  numero := StrToIntDef('abc', 0);  // Retorna 0 se não conseguir converter
  
  // FloatToStr
  texto := FloatToStr(3.14);
  texto := FloatToStrF(3.14159, ffFixed, 15, 2);  // 2 casas decimais = "3.14"
end;
```

---

## 12. Principais Diferenças

| Recurso | Python/C# | Delphi |
|---------|-----------|--------|
| **Índice de arrays** | Começa em 0 | Começa em 0 (mas Copy/Pos em 1!) |
| **Strings** | Aspas duplas ou simples | Apenas aspas simples |
| **Atribuição** | `=` | `:=` |
| **Comparação** | `==` | `=` |
| **Boolean** | `true/false` | `True/False` |
| **Null** | `None/null` | `nil` |
| **Comentário linha** | `#` ou `//` | `//` |
| **Comentário bloco** | `"""` ou `/* */` | `{ }` ou `(* *)` |
| **Case sensitive** | Sim | Não |
| **Garbage Collector** | Automático | Manual (precisa .Free) |
| **Operador ternário** | `x if y else z` | `IfThen(y, x, z)` |

---

## 13. Convenções de Nomenclatura Delphi

```pascal
type
  TMinhaClasse = class        // T = Type
  private
    FNome: string;            // F = Field (campo privado)
    FIdade: Integer;
  public
    constructor Create;       // Sempre "Create"
    destructor Destroy;       // Sempre "Destroy"
    procedure MinhaProc;
  end;

var
  LVariavelLocal: string;     // L = Local
  GVariavelGlobal: string;    // G = Global

const
  CONSTANTE = 100;            // MAIÚSCULA

procedure MinhaProc(AParametro: string);  // A = Argument
begin
  // código
end;
```

---

## 14. Memory Management (IMPORTANTE!)

Em **Python** e **C#**: Garbage Collector automático
Em **Delphi**: Manual!

```pascal
// ❌ ERRADO - Memory Leak!
var
  obj: TObject;
begin
  obj := TObject.Create;
  // ... usa obj ...
  // ESQUECEU de dar Free!
end;

// ✅ CORRETO
var
  obj: TObject;
begin
  obj := TObject.Create;
  try
    // ... usa obj ...
  finally
    obj.Free;  // SEMPRE libera memória
  end;
end;

// ✅ AINDA MELHOR (Delphi 10.4+)
var
  obj: TObject;
begin
  obj := TObject.Create;
  try
    // ... usa obj ...
  finally
    obj.DisposeOf;  // Mais seguro que Free
  end;
end;
```

**Regra de ouro**: Se você criou com `.Create`, você deve destruir com `.Free`!

---

## 15. Exemplo Completo Comparativo

### Objetivo: Ler JSON de uma API e processar

**Python:**
```python
import requests
import json

response = requests.get('https://api.example.com/users')
users = response.json()

for user in users:
    if user['age'] >= 18:
        print(f"Nome: {user['name']}, Idade: {user['age']}")
```

**Delphi:**
```pascal
uses System.JSON, RESTRequest4D;

var
  LResponse: IResponse;
  LJson: TJSONArray;
  LItem: TJSONObject;
  i: Integer;
  nome: string;
  idade: Integer;
begin
  LResponse := TRequest.New
    .BaseURL('https://api.example.com/users')
    .Accept('application/json')
    .Get;
  
  LJson := TJSONObject.ParseJSONValue(LResponse.Content) as TJSONArray;
  try
    for i := 0 to LJson.Count - 1 do
    begin
      LItem := LJson.Items[i] as TJSONObject;
      nome := LItem.GetValue<string>('name');
      idade := LItem.GetValue<Integer>('age');
      
      if idade >= 18 then
        Writeln(Format('Nome: %s, Idade: %d', [nome, idade]));
    end;
  finally
    LJson.Free;
  end;
end;
```

---

## 🎓 Resumo para Começar

1. **`:=`** é atribuição (não `=`)
2. **`begin/end`** são as chaves `{ }` do Delphi
3. **Sempre use `try/finally` e `.Free`** para objetos criados
4. **Índices começam em 0** (mas `Copy` e `Pos` em 1!)
5. **Strings usam aspas simples** `'texto'`
6. **Case-insensitive**: `writeln` = `Writeln` = `WRITELN`
7. **`Result`** é a variável de retorno de funções
8. **Property** é como getter/setter automático

Agora você está pronto para programar em Delphi! 🚀
