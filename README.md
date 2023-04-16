# exercise.java
import java.util.*;

public class SenhaDaVoZinha {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Leitura dos parâmetros de entrada
        int n = sc.nextInt(); // número de caracteres da senha
        int m = sc.nextInt(); // número de letras borradas da senha
        int k = sc.nextInt(); // comprimento de cada palavra
        String senha = sc.next(); // senha escrita no papel
        String[] palavras = new String[m]; // lista de palavras para substituir as letras borradas
        for (int i = 0; i < m; i++) {
            palavras[i] = sc.next();
        }
        int p = sc.nextInt(); // número de ordem da senha correta

        // Gerando todas as senhas possíveis
        List<String> senhas = gerarSenhas(senha, palavras);

        // Ordenando as senhas em ordem lexicográfica crescente
        Collections.sort(senhas);

        // Exibindo a senha correta
        System.out.println(senhas.get(p-1));
    }

    // Método que gera todas as senhas possíveis
    private static List<String> gerarSenhas(String senha, String[] palavras) {
        List<String> senhas = new ArrayList<>();
        gerarSenhasRec(senha, palavras, 0, "", senhas);
        return senhas;
    }

    // Método recursivo que gera as senhas possíveis
    private static void gerarSenhasRec(String senha, String[] palavras, int index, String tentativa, List<String> senhas) {
        if (index == senha.length()) {
            senhas.add(tentativa);
            return;
        }

        char c = senha.charAt(index);
        if (c == '#') {
            for (int i = 0; i < palavras.length; i++) {
                for (int j = 0; j < palavras[i].length(); j++) {
                    gerarSenhasRec(senha, palavras, index+1, tentativa + palavras[i].charAt(j), senhas);
                }
            }
        } else {
            gerarSenhasRec(senha, palavras, index+1, tentativa + c, senhas);
        }
    }
}
