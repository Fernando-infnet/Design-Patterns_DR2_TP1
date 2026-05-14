<img width="468" height="397" alt="image" src="https://github.com/user-attachments/assets/ba9f88b1-b35f-4aa3-8d5a-4139274310a7" />

Diagrama antigo

---

<img width="1613" height="1027" alt="Screenshot_20260514_092813" src="https://github.com/user-attachments/assets/64df9477-ed74-42a9-a6c7-ce672ba7f146" />

1. Singleton – Classe Library

A classe Library agora implementa o padrão Singleton (construtor privado + método estático getInstance()). Todas as operações de gerenciamento de itens, usuários e empréstimos passam por essa única instância. 
Isso evita que múltiplas instâncias de “Library” existam no sistema, eliminando a necessidade de passar referências entre classes.

2. Factory Method – Criação de itens (ItemFactory)

Como foi aplicado: Criada a classe abstrata ItemFactory com o método createItem(type, details). Atualmente suporta Book e DVD. Novas subclasses (ex.: MagazineFactory) ou extensão do método permitem adicionar novos tipos sem alterar o código cliente.
Problemas resolvidos:
Dificuldades de manutenção: Adicionar um novo tipo de item (DVD, Revista, E-book etc.) exige apenas uma nova entrada no Factory — nenhuma classe existente (Library, Loan, Facade) precisa ser modificada.
Repetição de código: Elimina os if/else ou switch espalhados para criar objetos Book vs DVD.
Alto acoplamento: O cliente (Facade/Library) não conhece as classes concretas Book/DVD — depende apenas da abstração Item.


3. Facade – LibraryFacade

Classe LibraryFacade expõe métodos simples e de alto nível (addBook, borrowItem, searchItems, getOverdueLoans etc.). Todo o acesso interno (Singleton Library + gerenciadores) fica oculto.
Clientes interagem apenas com a Facade nunca tocam diretamente em LoanManager, SearchService ou Library.

4. Observer – Notificações de empréstimos vencidos 

LoanManager é o Subject. Quando checkAndNotifyOverdues() identifica um empréstimo vencido, ele notifica todos os Observer registrados.

5. Strategy – Algoritmos de busca

Interface SearchStrategy com implementações concretas (TitleSearchStrategy, AuthorSearchStrategy). O SearchService recebe a estratégia em tempo de execução.
O algoritmo de busca está isolado; a LibraryFacade e o SearchService não precisam conhecer os detalhes de cada algoritmo.
