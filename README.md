# Explorador de funções

Aplicação educativa para editar funções matemáticas e comparar seus gráficos no plano cartesiano. O projeto usa HTML, CSS e JavaScript nativos, sem frameworks ou dependências externas.

## Como abrir

Abra `index.html` diretamente no navegador. Ele reúne HTML, CSS e JavaScript em um arquivo pronto para uso. `standalone.html` é uma cópia equivalente.

Para trabalhar com a versão modular, use `modular.html` junto de `styles.css` e dos módulos em `js/`. Sirva a pasta via servidor local:

```sh
python3 -m http.server 8000
```

Depois acesse `http://localhost:8000/modular.html`.

## Recursos

- Biblioteca de funções lineares, quadráticas, seno, exponencial, modular (valor absoluto) e logarítmica natural, com equações-base visíveis.
- Seletor de tipo para trocar a definição da função ativa.
- Controles deslizantes e campos numéricos sincronizados para cada coeficiente.
- Expressões personalizadas com edição em tempo real.
- Campo opcional para descrever funções simples em português e converter a descrição em uma expressão editável. Exemplo: `Função modular y(x) = módulo do módulo de x menos um` gera `abs(abs(x) - 1)`.
- Múltiplas curvas com cores e estilos de linha distintos.
- Controles para ocultar, mostrar e remover funções.
- Limites editáveis dos eixos cartesianos.
- Interface responsiva, navegação por teclado e mensagens acessíveis.

## Sintaxe permitida

Variável `x`, parâmetros `a`, `b`, `c`, `m`, `A`, `omega`, `phi`, `d`, `k` e `h`, constantes `pi` e `e`, números decimais e os operadores `+`, `-`, `*`, `/`, `^`. Multiplicação deve ser escrita com `*` (por exemplo, `2*x`). Funções de um argumento: `sin`, `cos`, `tan`, `sqrt`, `abs`, `log` (logaritmo natural) e `exp`. Funções trigonométricas usam radianos.

## Equações da biblioteca

- Linear: `y = m·x + b` (inclinação e intercepto).
- Quadrática: `y = a·x² + b·x + c` (termos quadrático, linear e constante).
- Seno: `y = A·sin(ω·x + φ) + d` (amplitude, frequência angular, fase e deslocamento vertical).
- Exponencial: `y = A·e^(k·x) + c` (escala, taxa de crescimento e deslocamento vertical).
- Modular: `y = a·|x − h| + k` (abertura/orientação e deslocamentos horizontal e vertical).
- Logarítmica: `y = a·ln(x − h) + k` (escala/orientação e deslocamentos horizontal e vertical; domínio `x > h`).

Os controles deslizantes atualizam o gráfico a cada movimento; o campo numérico correspondente permite inserir um valor exato.

Entradas de expressão são tokenizadas e convertidas em uma árvore sintática limitada. O avaliador executa somente operações e funções permitidas; ele não executa JavaScript arbitrário. Cada função recebe até 720 amostras por redesenho, e a aplicação aceita até 10 curvas visíveis na lista.

O conversor de linguagem humana usa regras locais e determinísticas, sem serviço externo. Ele cobre frases simples com `módulo`, `seno`, `cosseno`, `tangente`, `raiz quadrada`, `logaritmo natural`, números de zero a dez e operações como mais, menos, vezes e dividido por. A expressão resultante aparece no campo matemático e pode ser conferida ou ajustada. Descrições ambíguas ou fora desse conjunto devem ser escritas diretamente na sintaxe matemática indicada acima.

## Estrutura

- `index.html`: estrutura semântica e componentes da interface.
- `styles.css`: layout, acessibilidade visual e responsividade.
- `js/app.js`: estado e interação da aplicação.
- `js/functions.js`: catálogo, parâmetros e paleta.
- `js/expression-parser.js`: parser restrito e avaliador.
- `js/natural-language.js`: conversão de frases matemáticas simples em expressões permitidas.
- `js/graph.js`: eixos, marcas, amostragem e desenho SVG.
