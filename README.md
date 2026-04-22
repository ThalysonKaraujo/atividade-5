# Laboratório de Comunicação Inter-Frames e Segurança Web

## 1. Visão Geral do Projeto

Este projeto foi desenvolvido como uma atividade acadêmica para demonstrar a manipulação avançada do **DOM (Document Object Model)** entre diferentes contextos de navegação. A aplicação utiliza uma arquitetura baseada em frames para explorar como o JavaScript pode interagir com elementos de janelas distintas dentro da mesma origem.

### Estrutura de Arquivos:

- **`index.html` (O Hospedeiro):** Define a hierarquia da aplicação e organiza o layout utilizando `iframes`.
- **`frame1.html` (O Controlador):** Concentra **100% da lógica JavaScript**. Ele monitora a si mesmo e o frame vizinho, atuando como o núcleo inteligente do laboratório.
- **`frame2.html` (O Componente Passivo):** Um documento HTML puro, sem scripts internos, utilizado para validar a capacidade de controle remoto via DOM.

---

## 2. Justificativa de Segurança e Arquitetura

A implementação centralizada no **Frame 1** funciona como um estudo de caso sobre segurança de aplicações web:

### Same-Origin Policy (SOP)

O projeto demonstra que, quando dois frames residem no mesmo domínio, protocolo e porta, o navegador permite o acesso ao contexto de execução um do outro.

### Vulnerabilidades Exploradas (Cenário Controlado):

1. **Cross-Frame Scripting (XFS):** Demonstramos como um script em um contexto (Frame 1) pode ler dados sensíveis e interceptar eventos (clicks) em outro contexto (Frame 2).
2. **Riscos de XSS:** Se o Frame 1 for comprometido, o invasor ganha controle automático sobre as interações no Frame 2.
3. **Mecânicas de Clickjacking:** A capacidade de anexar um `onclick` em um botão externo a partir de outro frame evidencia a necessidade de cabeçalhos como `X-Frame-Options: DENY` em sistemas críticos.

---

## 3. Funcionamento Lógico

O fluxo de comunicação segue a seguinte lógica:

1. **Fluxo I (F1 -> F2):** O script no Frame 1 captura o valor de seu `textarea` e, via `window.parent.frames`, injeta o dado diretamente no DOM do Frame 2.
2. **Fluxo II (F2 -> F1):** Como o Frame 2 é passivo, o Frame 1 utiliza um _listener_ de carregamento (`onload`) para "sequestrar" o evento de clique do botão do Frame 2 e executar a cópia reversa.

---

## 4. Como Executar o Laboratório

Para evitar restrições de segurança de arquivos locais (CORS), utilize um servidor local:

1. Certifique-se de ter o **VS Code** instalado com a extensão **Live Server**.
2. Abra a pasta do projeto no VS Code.
3. Clique em **"Go Live"** no canto inferior direito.
4. Acesse: `http://127.0.0.1:5500/index.html`.

---

### Atividade 5 - Segurança de Sistemas

**Estudante:** Thalyson Kauan Araújo  
**Instituição:** UFRPE  
**Contexto:** Preparação para a 1ª VA
