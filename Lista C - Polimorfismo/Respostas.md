# Respostas Lista C - Polimorfismo

## 1.a) O que é polimorfismo?

Capacidade de uma função, método ou objeto de se comportar de diferentes maneiras dependendo do contexto.

## 1.b)

### Late binding

Ocorre quando o método a ser chamado é decidido em tempo de execução, baseado no tipo do objeto que está sendo referenciado.

```java
class Conta {
    public void sacar(double valor) {
        System.out.println("Saque de conta");
    }
}

class ContaCorrente extends Conta {
    @Override
    public void sacar(double valor) {
        System.out.println("Saque de conta corrente");
    }

public class Main {
    public static void main(String[] args) {
        Conta conta = new ContaCorrente();
        conta.sacar(100);
    }
}

```

### Early binding

Ocorre quando o método a ser chamado é decidido em tempo de compilação, baseado no tipo da referência.

```java
class Conta {
    public void sacar(double valor) {
        System.out.println("Saque de conta");
    }
}

class ContaCorrente extends Conta {
    public void sacar(double valor) {
        System.out.println("Saque de conta corrente");
    }
}

public class Main {
    public static void main(String[] args) {
        Conta conta = new Conta();
        conta.sacar(100);

        ContaCorrente contaCorrente = new ContaCorrente();
        contaCorrente.sacar(100);
    }
}

```

## 2) Explique como funcionam as (tentativas de) conversões entre tipos polimórficos, isto é, upcasting e downcasting. Dê exemplos em código-fonte. Quando devemos usar um ou o outro ao criar um programa de computador?

### Upcasting

Conversao de subclass para superclasse. Sempre é possível fazer upcasting, pois a subclasse é um tipo da superclasse. O exemplo anterior já mostra um exemplo de upcasting.

```java
class Conta {
    public void sacar(double valor) {
        System.out.println("Saque de conta");
    }
}

class ContaCorrente extends Conta {
    public void sacar(double valor) {
        System.out.println("Saque de conta corrente");
    }
}

public class Main {
    public static void main(String[] args) {
        Conta conta = new ContaCorrente();//upcasting
        conta.sacar(100);
    }
}
```

### Downcasting

Conversão de superclasse para subclasse. Nem sempre é possível fazer downcasting, pois a superclasse não é necessariamente um tipo da subclasse. Para fazer downcasting é necessário fazer um cast explícito.

```java

class Conta {
    public void sacar(double valor) {
        System.out.println("Saque de conta");
    }
}

class ContaCorrente extends Conta {
    public void sacar(double valor) {
        System.out.println("Saque de conta corrente");
    }
}

public class Main {
    public static void main(String[] args) {
        Conta conta = new ContaCorrente();
        ContaCorrente contaCorrente = (ContaCorrente) conta;//downcasting
        contaCorrente.sacar(100);
    }
}
```

## 3) O que é um método abstrato? Dê um exemplo em código-fonte.

Método abstrato é um método que não possui implementação, apenas a assinatura. A implementação é feita pelas subclasses.

Para que Serve?

- Definir uma interface comum para um grupo de subclasses.
- Fornecer uma implementação padrão para alguns métodos, enquanto outros métodos são deixados para serem implementados pelas subclasses.
- Facilitar o uso do polimorfismo, permitindo que objetos de diferentes subclasses sejam tratados de maneira uniforme

```java

abstract class Conta {
    public abstract void sacar(double valor);

    public void depositar(double valor) {
        System.out.println("Deposito de conta");
    }
}

class ContaCorrente extends Conta {
    @Override
    public void sacar(double valor) {
        System.out.println("Saque de conta corrente");
    }
}

public class Main {
    public static void main(String[] args) {
        Conta conta = new ContaCorrente();
        conta.sacar(100);
    }
}
```

## 4) Qual o propósito das interfaces em POO? Liste e explique as diferenças entre interfaces e classes abstratas (e.g., crie uma tabela comparativa). Também discuta sobre como as diferentes linguagem podem entregar essa característica da POO de formas diferentes.

### Propósito das interfaces

- Definir um contrato que as classes devem seguir.
- Permitir que objetos de diferentes classes sejam tratados de maneira uniforme.

### Diferenças entre Interfaces e Classes Abstratas

| Característica          | Interface                                      | Classe Abstrata                                |
|-------------------------|------------------------------------------------|------------------------------------------------|
| Instanciação            | Não pode ser instanciada                       | Não pode ser instanciada                       |
| Métodos                 | Apenas métodos abstratos (até Java 7)          | Pode ter métodos abstratos e concretos         |
| Implementação de Métodos| Não pode ter implementação (até Java 7)        | Pode ter implementação                         |
| Herança                 | Pode ser implementada por qualquer classe      | Pode ser estendida por uma classe              |
| Múltipla Herança        | Uma classe pode implementar várias interfaces | Uma classe pode estender apenas uma classe     |
| Modificadores de Acesso | Métodos são implicitamente públicos e abstratos| Pode ter modificadores de acesso               |
| Propriedades            | Não pode ter propriedades                      | Pode ter propriedades                          |

## 5)Desenvolva um programa simples (ou não, isso fica ao seu critério) que utilize os conceitos de interface e classe abstrata como formas de favorecer (ou forçar) o polimorfismo. 

```java

interface Veiculo {
    void mover();
}

abstract class Carro implements Veiculo {
    @Override
    public void mover() {
        System.out.println("Carro está se movendo");
    }
}


class Sedan extends Carro {
    @Override
    public void mover() {
        System.out.println("Sedan está se movendo");
    }
}


public class Main {
    public static void main(String[] args) {
        Veiculo meuCarro = new Sedan();
        meuCarro.mover();
    }
}

```

