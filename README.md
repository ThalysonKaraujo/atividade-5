# Laboratório de Comunicação Inter-Frames e Segurança Web

## 1. Visão Geral do Projeto

Este projeto foi desenvolvido como uma atividade acadêmica para demonstrar a manipulação avançada do **DOM (Document Object Model)** entre diferentes contextos de navegação. A aplicação utiliza uma arquitetura baseada em frames para explorar como o JavaScript pode interagir com elementos de janelas distintas dentro da mesma origem.

### Estrutura de Arquivos:

- **`index.html` (O Hospedeiro):** Define a hierarquia da aplicação e organiza o layout utilizando `iframes`.
- **`frame1.html` (O Controlador):** Concentra **100% da lógica JavaScript**. Ele monitora a si mesmo e o frame vizinho, atuando como o núcleo inteligente do laboratório.
- **`frame2.html` (O Componente Passivo):** Um documento HTML puro, sem scripts internos, utilizado para validar a capacidade de controle remoto via DOM.

---

## 2. Justificativa de Segurança e Arquitetura

A implementação centralizada no **Frame 1** não é apenas uma escolha de design, mas um estudo de caso sobre segurança de aplicações web:

### Same-Origin Policy (SOP)

O projeto demonstra que, quando dois frames residem no mesmo domínio, protocolo e porta, o navegador permite o acesso total ao contexto de execução um do outro.

### Vulnerabilidades Exploradas (Cenário Controlado):

1.  **Cross-Frame Scripting (XFS):** Demonstramos como um script em um contexto (Frame 1) pode ler dados sensíveis (input de texto) e interceptar eventos (clicks) em outro contexto (Frame 2).
2.  **Riscos de XSS:** Se o Frame 1 for comprometido por uma injeção de script, o invasor ganha controle automático sobre todas as interações do usuário no Frame 2.
3.  **Mecânicas de Clickjacking:** A capacidade de anexar um `onclick` em um botão externo (`btnFrame2`) a partir de outro frame evidencia por que desenvolvedores devem utilizar cabeçalhos de segurança como `X-Frame-Options: DENY` ou `Content-Security-Policy: frame-ancestors 'none'` em aplicações críticas.

---

## 3. Funcionamento Lógico

O fluxo de comunicação segue a seguinte lógica de programação:

1.  **Fluxo I (F1 -> F2):** O script no Frame 1 captura o valor de seu `textarea` local e, via `window.parent.frames`, injeta o valor diretamente no DOM do Frame 2.
2.  **Fluxo II (F2 -> F1):** Como o Frame 2 não possui scripts, o Frame 1 utiliza um _listener_ de carregamento (`onload`) para detectar quando o Frame 2 está pronto. Após isso, ele "sequestra" o evento de clique do botão do Frame 2 para executar a função de cópia reversa.

---

## 4. Como Executar o Laboratório

Para evitar restrições de segurança de arquivos locais (CORS) em navegadores modernos, recomenda-se a execução via servidor local:

1.  Certifique-se de ter o **VS Code** instalado.
2.  Instale a extensão **Live Server**.
3.  Abra a pasta do projeto e clique em **"Go Live"** no canto inferior direito.
4.  Acesse a aplicação via `http://127.0.0.1:5500/index.html`.

---

**Desenvolvido para a disciplina de Segurança de Sistemas / Desenvolvimento Web.**
