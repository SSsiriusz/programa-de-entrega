# programa-de-entrega
package ProgramaDeEntrega;

import java.util.HashMap;
import java.util.Map;

public class EmpresaEntregas {
    private Map<String, Pedido> pedidos;

    public EmpresaEntregas() {
        this.pedidos = new HashMap<>();
    }

    public void adicionarPedido(Pedido pedido) {
        pedidos.put(pedido.getCodigo(), pedido);
    }

    public Pedido buscarPedido(String codigo) {
        return pedidos.get(codigo);
    }
}
package ProgramaDeEntrega;

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        EmpresaEntregas empresa = new EmpresaEntregas();

        Pedido pedido1 = new Pedido("001", StatusPedido.PENDENTE);
        Pedido pedido2 = new Pedido("002", StatusPedido.EM_TRANSPORTE);
        Pedido pedido3 = new Pedido("003", StatusPedido.ENTREGUE);
        Pedido pedido4 = new Pedido("004", StatusPedido.CANCELADO);

        pedido1.adicionarProduto(new Produto("Notebook", 3500.00));
        pedido1.adicionarProduto(new Produto("Mouse", 150.00));

        pedido2.adicionarProduto(new Produto("Celular", 2500.00));

        pedido3.adicionarProduto(new Produto("Câmera", 1800.00));

        pedido4.adicionarProduto(new Produto("Fone de ouvido", 200.00));

        empresa.adicionarPedido(pedido1);
        empresa.adicionarPedido(pedido2);
        empresa.adicionarPedido(pedido3);
        empresa.adicionarPedido(pedido4);

        Scanner scanner = new Scanner(System.in);
        System.out.print("Digite o código do pedido: ");
        String codigo = scanner.nextLine();

        Pedido pedidoEncontrado = empresa.buscarPedido(codigo);
        if (pedidoEncontrado != null) {
            pedidoEncontrado.mostrarDetalhes();
        } else {
            System.out.println("Pedido não encontrado.");
        }
    }
}
package ProgramaDeEntrega;

import java.util.ArrayList;
import java.util.List;

public class Pedido {
    private String codigo;
    private StatusPedido status;
    private List<Produto> produtos;

    public Pedido(String codigo,StatusPedido status) {
        this.codigo = codigo;
        this.status = status;
        this.produtos = new ArrayList<>();
    }

    public String getCodigo() {
        return codigo;
    }
    public StatusPedido getStatus() {
        return status;
    }
    public void adicionarProduto(Produto produto) {
        produtos.add(produto);
    }
    public void mostrarDetalhes() {
        System.out.println("Pedido: " + codigo);
        System.out.println("Status: " + status);
        System.out.println("Produtos: ");
        for (Produto p : produtos) {
            System.out.println("- " + p);
        }
    }
}
package ProgramaDeEntrega;

public class Produto {
    private String nome;
    private double preço;

    public Produto(String nome, double preço) {
        this.nome = nome;
        this.preço = preço;
    }
    public String getNome(){
        return nome;
    }
    public double getPreco() {
        return preço;
    }
    @Override
    public String toString() {
        return nome + " - R$ " + preço;
    }
}
package ProgramaDeEntrega;

public enum StatusPedido {
    PENDENTE,
    EM_TRANSPORTE,
    ENTREGUE,
    CANCELADO
}
