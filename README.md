import java.util.*;

class Aluno implements Comparable<Aluno> {
    private int matricula;
    private String nome;
    private double nota;

    public Aluno(int matricula, String nome, double nota) {
        this.matricula = matricula;
        this.nome = nome;
        this.nota = nota;
    }

    public int getMatricula() { return matricula; }
    public String getNome() { return nome; }
    public double getNota() { return nota; }

    @Override
    public String toString() {
        return "Aluno{" + "matricula=" + matricula + ", nome='" + nome + '\'' + ", nota=" + nota + '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Aluno aluno = (Aluno) o;
        return matricula == aluno.matricula;
    }

    @Override
    public int hashCode() {
        return Objects.hash(matricula);
    }

    @Override
    public int compareTo(Aluno outro) {
        return this.nome.compareTo(outro.nome);
    }
}

public class SistemaCadastroAlunos {

    public static void main(String[] args) {
        System.out.println("=== SISTEMA DE CADASTRO DE ALUNOS ===");


        System.out.println("\n--- 1. ARRAYLIST (Histórico de Acessos) ---");
        List<String> historicoAcessos = new ArrayList<>();

        historicoAcessos.add("João (Login)");
        historicoAcessos.add("Maria (Login)");
        historicoAcessos.add("João (Logout)"); // Demonstra permissão de duplicidade lógica

        if(historicoAcessos.contains("João (Logout)")) {
            historicoAcessos.remove("João (Logout)");
        }

        for (String acesso : historicoAcessos) {
            System.out.println(acesso);
        }


        System.out.println("\n--- 2. LINKEDLIST (Fila de Espera) ---");
        LinkedList<String> filaEspera = new LinkedList<>();

        filaEspera.addLast("Carlos");
        filaEspera.addLast("Ana");
        filaEspera.addLast("Pedro");

        System.out.println("A Ana está na fila? " + filaEspera.contains("Ana"));

        String atendido = filaEspera.pollFirst();
        System.out.println("Atendido: " + atendido);

        System.out.println("Restantes na fila:");
        for (String pessoa : filaEspera) {
            System.out.println("- " + pessoa);
        }


        System.out.println("\n--- 3. HASHSET (Controle de CPFs Únicos) ---");
        Set<String> cpfsCadastrados = new HashSet<>();


        cpfsCadastrados.add("111.111.111-11");
        cpfsCadastrados.add("222.222.222-22");


        boolean adicionouDuplicado = cpfsCadastrados.add("111.111.111-11");
        System.out.println("Conseguiu adicionar CPF duplicado? " + adicionouDuplicado);


        if (cpfsCadastrados.contains("222.222.222-22")) {
            cpfsCadastrados.remove("222.222.222-22");
        }


        for (String cpf : cpfsCadastrados) {
            System.out.println("CPF válido: " + cpf);
        }


        System.out.println("\n--- 4. TREESET (Ranking Alfabético) ---");
        Set<Aluno> alunosOrdenados = new TreeSet<>();

        Aluno a1 = new Aluno(101, "Zeca", 8.5);
        Aluno a2 = new Aluno(102, "Amanda", 9.0);
        Aluno a3 = new Aluno(103, "Bruno", 7.5);

        alunosOrdenados.add(a1);
        alunosOrdenados.add(a2);
        alunosOrdenados.add(a3);

        alunosOrdenados.remove(a3);


        for (Aluno aluno : alunosOrdenados) {
            System.out.println(aluno.getNome() + " - " + aluno.getNota());
        }

        System.out.println("\n--- 5. HASHMAP (Busca de Aluno por Matrícula) ---");
        Map<Integer, Aluno> mapaAlunos = new HashMap<>();

        mapaAlunos.put(a1.getMatricula(), a1);
        mapaAlunos.put(a2.getMatricula(), a2);

        Aluno alunoEncontrado = mapaAlunos.get(101);
        System.out.println("Aluno matricula 101 encontrado: " + alunoEncontrado.getNome());

        mapaAlunos.remove(102);

        for (Map.Entry<Integer, Aluno> entry : mapaAlunos.entrySet()) {
            System.out.println("Chave: " + entry.getKey() + " | Valor: " + entry.getValue().getNome());
        }

        System.out.println("\n--- 6. TREEMAP (Matrículas Ordenadas) ---");
        Map<Integer, Aluno> mapaOrdenado = new TreeMap<>();

        mapaOrdenado.put(999, new Aluno(999, "Thiago", 6.0));
        mapaOrdenado.put(100, new Aluno(100, "Beatriz", 9.5));
        mapaOrdenado.put(500, new Aluno(500, "Daniel", 8.0));

        System.out.println("Existe a matrícula 500? " + mapaOrdenado.containsKey(500));
        mapaOrdenado.remove(999);

        for (Integer matricula : mapaOrdenado.keySet()) {
            System.out.println("Matrícula: " + matricula + " -> " + mapaOrdenado.get(matricula).getNome());
        }
    }
}
