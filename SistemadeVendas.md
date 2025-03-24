# Sistema de Vendas Simples
**Requisitos básicos:** <br>
O vendedor pode buscar um livro pelo título ou autor. <br>
O sistema lista os livros que atendem aos critérios da busca. <br>
O vendedor seleciona um livro e informa a quantidade vendida. <br>
O sistema adiciona o livro à venda atual e mostra o subtotal. <br>
O vendedor pode repetir os passos 1-4 para adicionar mais livros à venda. <br>
O vendedor conclui a venda e o sistema calcula o total. <br>
O sistema emite uma nota fiscal para o cliente. <br>
### Tarefa 1: Diagrama de Caso de Uso<br>
Desenhe um diagrama de caso de uso representando as operações descritas nos requisitos básicos.
```plantuml
@startuml name
left to right direction
actor Vendedor
rectangle Sistema {
  usecase "Buscar Livro" as UC1
  usecase "Adicionar à Venda" as UC2
  usecase "Concluir Venda" as UC3
  usecase "Emitir Nota Fiscal" as UC4
}
Vendedor --> UC1
Vendedor --> UC2
Vendedor --> UC3
Vendedor --> UC4
@enduml
```
### Tarefa 2: Diagrama de Classes
Identifique as classes envolvidas neste sistema e suas relações e crie um diagrama de classes. Lembre-se de considerar atributos e métodos básicos para as classes.
```mermaid
classDiagram
    class Vendedor {
        +String nome
        +int id
        +buscarLivro()
        +adicionarLivroAVenda()
    }

    class Livro {
        +String titulo
        +String autor
        +float preco
        +int estoque
    }

    class Venda {
        +int id
        +DateTime data
        +float total
        +calcularTotal()
        +emitirNotaFiscal()
    }

    class ItemVenda {
        +int quantidade
        +float subtotal
        +calcularSubtotal()
    }

    Vendedor "1" --> "0..*" Venda : Realiza
    Venda "1" --> "1..*" ItemVenda : Contém
    ItemVenda "1" --> "1" Livro : Inclui
```
### Tarefa 3: Diagrama de Sequência
Escolha uma das operações (por exemplo, "Concluir Venda") e ilustre-a usando um diagrama de sequência. Garanta que a interação entre os objetos e os atores esteja claramente representada.
```mermaid
sequenceDiagram
    actor Vendedor
    participant Sistema
    participant Venda
    participant NotaFiscal

    Vendedor ->> Sistema: Solicita concluir venda
    Sistema ->> Venda: calcularTotal()
    Venda -->> Sistema: Total da venda (R$ 150,00)
    Sistema ->> NotaFiscal: emitir()
    NotaFiscal -->> Sistema: Nota fiscal gerada (PDF)
    Sistema -->> Vendedor: Exibe confirmação e nota fiscal
```