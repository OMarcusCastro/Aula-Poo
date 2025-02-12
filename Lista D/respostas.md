# 1.Propósito dos membros static

Os atributos e métodos estáticos pertencem à classe, e não a uma instância individual. Isso permite que eles sejam acessados sem a necessidade de criar objetos; são úteis para definir comportamentos ou estados compartilhados por todas as instâncias, como constantes, contadores globais, ou métodos utilitários.

## Vantagens:

- Acesso direto sem instanciar a classe.
- Consistência de dados quando o estado for compartilhado (ex.: contador de instâncias).
- Ideal para métodos utilitários (como `Math.sqrt()`).

## Desvantagens:

- Dificuldade em realizar testes unitários e simulações (dificulta a injeção de dependência).
- Estado global pode levar a problemas de concorrência e dificultar o rastreamento de mudanças.
- Menor flexibilidade na utilização de polimorfismo.

```java
public class Contador {
    private static int totalInstancias = 0;

    public Contador() {
        totalInstancias++;
    }

    public static int getTotalInstancias() {
        return totalInstancias;
    }

    public static void resetarContador() {
        totalInstancias = 0;
    }
}

public class MainStatic {
    public static void main(String[] args) {
        new Contador();
        new Contador();
        System.out.println("Total de instâncias criadas: " + Contador.getTotalInstancias());
        Contador.resetarContador();
        System.out.println("Após reset, total: " + Contador.getTotalInstancias());
    }
}
```

---

## 2. Encapsulamento e sua relação com os outros pilares

Encapsulamento é o mecanismo de ocultar detalhes internos de uma classe, expondo apenas o que é necessário por meio de uma interface pública (geralmente por meio de métodos como getters e setters). Ele protege os dados internos contra modificações indevidas e permite que a implementação interna mude sem afetar os clientes da classe.

### Relação com os outros pilares:

- **Herança**: Através do encapsulamento, as subclasses herdam uma interface clara sem precisar conhecer a implementação interna da superclasse.
- **Polimorfismo**: Objetos encapsulados expõem operações padronizadas que podem ter implementações diferentes, possibilitando o polimorfismo.
- **Abstração**: Encapsulamento ajuda a ocultar a complexidade e expor apenas a funcionalidade essencial, promovendo a abstração.

---

## 3. Getters e Setters

Getters e Setters são métodos usados para acessar (**get**) e modificar (**set**) os atributos privados de uma classe. Eles promovem o encapsulamento, permitindo validar dados e controlar o acesso, ao invés de expor os atributos diretamente.

### Vantagens:

- Controle e validação da entrada de dados (ex.: impedir valores negativos).
- Possibilidade de implementar lógica adicional (ex.: notificar mudanças).
- Facilidade para manter e refatorar o código sem afetar os clientes da classe.

---

## 4. Programa simples combinando static e encapsulamento (Exemplo CRUD)

Para gerenciar o ciclo de vida de objetos, pode-se implementar um repositório que manipula uma coleção (por exemplo, `ArrayList`) de objetos. Utilizando membros `static`, esse repositório centraliza as operações de criação (**Create**), leitura (**Read**), atualização (**Update**) e remoção (**Delete**) de forma compartilhada.

### Discussão:

- Neste exemplo, o repositório de produtos mantém uma lista compartilhada de instâncias (**atributo static**).
- O atributo `proximoId` é também `static`, garantindo que cada novo produto receba um ID único, sem a necessidade de criar uma instância do repositório.
- O uso de getters e setters na classe `Produto` protege os atributos e permite validações ou lógica adicional se necessário.

---

Essas respostas e exemplos ilustram de forma prática os conceitos de `static`, encapsulamento, getters/setters e como combiná-los para implementar operações de CRUD em uma aplicação Java.
