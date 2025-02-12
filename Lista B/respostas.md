# Lista B

## 1.Quais são as associações presentes na UML? Quais são as propriedades dessas associações e como essas associações são implementadas no código-fonte (Java, C++ ou C#)? 

### Associação

Associação é um relacionamento entre classes que indica que um objeto de uma classe está relacionado com um objeto de outra classe.

```java
class Pessoa {
    private String nome;

    public Pessoa(String nome) {
        this.nome = nome;
    }

    public String getNome() {
        return nome;
    }
}

class Carro {
    private Pessoa dono;

    public Carro(Pessoa dono) {
        this.dono = dono;
    }

    public Pessoa getDono() {
        return dono;
    }
}

public class Main {
    public static void main(String[] args) {
        Pessoa pessoa = new Pessoa("João");
        Carro carro = new Carro(pessoa);
        System.out.println("Dono do carro: " + carro.getDono().getNome());
    }
}
```

### Agregação

Agregação é um tipo de associação que indica que um objeto de uma classe é parte de um objeto de outra classe.

```java

class Roda {
    private int aro;

    public Roda(int aro) {
        this.aro = aro;
    }

    public int getAro() {
        return aro;
    }
}

class Carro {
    private Roda[] rodas;

    public Carro(Roda[] rodas) {
        this.rodas = rodas;
    }

    public Roda[] getRodas() {
        return rodas;
    }
}
````

### Composição

Composição é um tipo de agregação que indica que um objeto de uma classe é parte de um objeto de outra classe e não pode existir sem ele.

```java
class Motor {
    private String tipo;

    public Motor(String tipo) {
        this.tipo = tipo;
    }

    public String getTipo() {
        return tipo;
    }
}

class Carro {
    private Motor motor;

    public Carro(String tipoMotor) {
        this.motor = new Motor(tipoMotor);
    }

    public Motor getMotor() {
        return motor;
    }
}

public class Main {
    public static void main(String[] args) {
        Carro carro = new Carro("V8");
        System.out.println("Tipo do motor: " + carro.getMotor().getTipo());
    }
}
```

## 2.Qual a diferença entre agregação e composição? Dê exemplos com código e UML.

- Agregação: Representa um relacionamento "todo/parte" onde a parte pode existir independentemente do todo. Exemplo: Universidade e Departamento.
- Composição: Representa um relacionamento "todo/parte" onde a parte não pode existir independentemente do todo. Exemplo: Carro e Motor.

```java

class Motor {
    private String tipo;

    public Motor(String tipo) {
        this.tipo = tipo;
    }

    public String getTipo() {
        return tipo;
    }
}

class Carro {
    private Motor motor;

    public Carro(String tipoMotor) {
        this.motor = new Motor(tipoMotor);
    }

    public Motor getMotor() {
        return motor;
    }
}

public class Main {
    public static void main(String[] args) {
        Carro carro = new Carro("V8");
        System.out.println("Tipo do motor: " + carro.getMotor().getTipo());
    }
}
```

## 3.a. Explique o que é herança. Explique como funcionam os mecanismos de sobreposição (override) e de sobrecarga (overload) de métodos.

### Herança

Herança é um mecanismo que permite que uma classe herde atributos e métodos de outra classe. A classe que herda é chamada de subclasse e a classe que é herdada é chamada de superclasse.

### Sobreposição (Override)

Sobreposição é um mecanismo que permite que uma subclasse forneça uma implementação específica para um método que já foi definido na superclasse. E tambem para indicar que ja houve uma implementação do método na superclasse.

### Sobrecarga (Overload)

Sobrecarga é um mecanismo que permite que uma classe tenha mais de um método com o mesmo nome, desde que suas assinaturas (número ou tipo de parâmetros) sejam diferentes. A sobrecarga é resolvida em tempo de compilação.

## 3.b. Implemente um pequeno programa ilustrando esses três conceitos. (2 pontos)

```java
class Conta {
    private double saldo;

    public Conta(double saldo) {
        this.saldo = saldo;
    }

    public double getSaldo() {
        return saldo;
    }

    public void sacar(double valor) {
        saldo -= valor;
    }

    public void depositar(double valor) {
        saldo += valor;
    }

    // Sobrecarga do método depositar
    public void depositar(double valor, String moeda) {
        if (moeda.equals("USD")) {
            saldo += valor * 5.0; // Supondo uma taxa de câmbio fictícia
        } else {
            saldo += valor;
        }
    }
}

class ContaCorrente extends Conta {
    private double limite;

    public ContaCorrente(double saldo, double limite) {
        super(saldo);
        this.limite = limite;
    }

    @Override
    public void sacar(double valor) {
        if (valor <= getSaldo() + limite) {
            super.sacar(valor);
        } else {
            System.out.println("Saldo insuficiente");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Conta conta = new Conta(1000);
        conta.depositar(500);
        System.out.println("Saldo após depósito: " + conta.getSaldo());

        conta.depositar(100, "USD");
        System.out.println("Saldo após depósito em USD: " + conta.getSaldo());

        ContaCorrente contaCorrente = new ContaCorrente(1000, 500);
        contaCorrente.sacar(1200);
        System.out.println("Saldo após saque: " + contaCorrente.getSaldo());

        contaCorrente.sacar(400);
        System.out.println("Saldo após saque: " + contaCorrente.getSaldo());
    }
}
```

## 4. Desenvolva uma discussão sobre o recurso de herança múltipla, seus perigos e suas oportunidades.

Facilidade de reutilização de código, mas pode levar a problemas de ambiguidade e complexidade. Em Java, a herança múltipla é proibida, mas é possível implementar interfaces para obter um comportamento semelhante.

## 5. Quais as vantagens e desvantagens de usar composição no lugar da herança? Essa é talvez a questão mais importante da disciplina! 

Vantagens:

- Maior flexibilidade
- Menor acoplamento
- Facilidade de reutilização de código

Desvantagens:

- Maior complexidade
- Maior quantidade de código
