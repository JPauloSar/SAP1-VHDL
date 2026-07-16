```markdown
# SAP-1: Planejamento, Diretrizes e Organização do Repositório

Este é um documento temporário de alinhamento interno para o desenvolvimento do nosso SAP-1 em VHDL e hardware físico. Ele estabelece a estrutura do projeto, as regras de versionamento e o fluxo de trabalho inicial que todos devemos seguir.

---

## 📂 Estrutura de Pastas

Para manter o repositório limpo e evitar conflitos de mesclagem (*merge conflicts*), utilizaremos estritamente a seguinte estrutura de diretórios:

```text
sap1-projeto/
├── doc/             # Documentação, diagramas de bloco e especificações de arquitetura
├── hdl/             # Código-fonte VHDL (.vhd, .vhdl) - Módulos do SAP-1
├── sim/             # Testbenches para simulação e validação
├── constraints/     # Arquivos de pinagem (.qsf para Quartus, .xdc para Vivado)
├── synth/           # Arquivos de projeto das ferramentas de FPGA (não versionar arquivos temporários)
├── schematics/      # Esquemáticos de hardware (Proteus, KiCad, etc.) para a protoboard
├── .gitignore       # Filtro de arquivos que não devem subir para o GitHub
├── CONTRIBUTORS.md  # Registro oficial de autoria e divisão de tarefas da equipe
├── LICENSE          # Termos de uso e proteção legal do projeto (Licença MIT)
└── README.md        # Este guia

```

---

## 🛠️ Regras de Versionamento e Fluxo de Trabalho

1. **Proteção da Branch `main`:** Nunca faça commits diretos na branch `main`. Toda alteração deve ser feita em uma branch separada e integrada via *Pull Request (PR)*.
2. **Uso do `.gitignore`:** Arquivos temporários de compilação, logs e binários gerados pelo Quartus, Vivado ou ModelSim não devem ser enviados ao repositório. O arquivo `.gitignore` na raiz já está configurado para filtrar esses arquivos automaticamente.
3. **Validação:** Qualquer módulo de hardware escrito na pasta `hdl/` só poderá ser integrado à `main` após a criação e validação do seu respectivo testbench na pasta `sim/`.

---

## 🚀 Passo a Passo: Primeiro Acesso e Validação do Fluxo

Para validarmos o fluxo de trabalho de todos na equipe antes do início do desenvolvimento dos blocos de hardware, realizaremos uma tarefa inicial simples: adicionar nossos nomes ao arquivo `CONTRIBUTORS.md`.

Siga os comandos abaixo no seu terminal para realizar este processo:

### Passo 1: Clonar o Repositório

Abra o terminal na pasta onde deseja salvar o projeto e execute:

```bash
git clone [https://github.com/JPauloSar/SAP1-VHDL.git](https://github.com/JPauloSar/SAP1-VHDL.git)
cd SAP1-VHDL

```

### Passo 2: Criar sua Branch Pessoal

Crie e mude para uma branch com o seu nome utilizando o padrão `feature/nome-sobrenome`:

```bash
git checkout -b feature/seu-nome

```

### Passo 3: Editar o Arquivo de Colaboradores

1. Abra o arquivo `CONTRIBUTORS.md`.
2. Substitua um dos campos de marcação (*placeholders* como "Amigo A") pelo seu **Nome Completo** e o link do seu **Perfil do GitHub**.
3. **Atenção:** Deixe a coluna de responsabilidades em branco por enquanto, pois faremos a divisão de tarefas posteriormente.
4. Salve o arquivo.

### Passo 4: Registrar e Enviar as Alterações

Adicione o arquivo modificado, crie o commit com uma mensagem clara e envie a branch para o GitHub:

```bash
git add CONTRIBUTORS.md
git commit -m "docs: adiciona [Seu Nome] aos contribuidores"
git push origin feature/seu-nome

```

### Passo 5: Abrir o Pull Request (PR)

1. Acesse a página do repositório no GitHub.
2. Clique no botão **"Compare & pull request"** que aparecerá na parte superior da tela.
3. Insira um título direto (ex: "Adiciona [Seu Nome] ao CONTRIBUTORS") e envie o PR.
4. O administrador do repositório revisará e fará o merge para a branch `main`.

---

## ⚖️ Implicações Legais e Direitos Autorais (Copyright)

A inclusão de nomes no arquivo `LICENSE` (sob a licença MIT) e no arquivo `CONTRIBUTORS.md` possui implicações jurídicas reais sobre a propriedade intelectual do projeto:

* **Coautoria e Propriedade Intelectual:** Perante as leis de direitos autorais (como a Lei nº 9.610/98 no Brasil e tratados internacionais), qualquer pessoa que escreva código para este repositório possui direitos morais e patrimoniais sobre a sua respectiva contribuição. A listagem oficial garante a autoria legal do seu trabalho para portfólio acadêmico e profissional.
* **Segurança Legal com a Licença MIT:** Ao adotarmos a licença MIT em conjunto com a lista de contribuidores, estabelecemos que:
1. Qualquer membro do grupo (ou terceiros, caso o repositório se torne público no futuro) tem permissão legal para usar, modificar e distribuir este código.
2. Ninguém poderá ser processado pelo uso do código, pois ele é fornecido "no estado em que se encontra" (*as is*), sem garantias.
3. Os créditos originais (os nomes listados) devem ser obrigatoriamente preservados em qualquer cópia ou derivação do projeto.



```

```
---

## 📂 Guia de Uso Prático das Pastas

Como este é o nosso primeiro projeto de hardware em equipe, usaremos as pastas da seguinte forma para manter o desenvolvimento organizado:

*   **`doc/` (Guia de Referência):** Aqui colocaremos as tabelas verdade da Unidade de Controle, a matriz de microinstruções (sinais de controle) e o conjunto de instruções (ISA) do nosso SAP-1. Sempre que houver uma alteração na arquitetura do processador, o documento nesta pasta deve ser atualizado.
*   **`hdl/` (Apenas Código Limpo):** Esta pasta deve conter apenas os arquivos de descrição física do hardware em VHDL (`.vhd` ou `.vhdl`). Nenhum arquivo gerado por compilador deve entrar aqui.
*   **`sim/` (Ambiente de Testes):** Aqui ficam os arquivos de teste (*testbenches*). Ao desenvolver a ALU, por exemplo, o arquivo `alu.vhd` fica em `hdl/` e o seu arquivo de teste `tb_alu.vhd` fica em `sim/`.
*   **`constraints/` (Mapeamento Físico):** Pasta exclusiva para os arquivos de atribuição de pinos da placa de desenvolvimento (FPGA). Só será alterada quando precisarmos mapear portas lógicas para os pinos físicos de entrada e saída.
*   **`synth/` (Ambiente de Síntese):** Reservada para os arquivos de projeto das ferramentas (como o arquivo `.qpf`/`.qsf` do Quartus ou `.xpr` do Vivado). O fluxo de trabalho aqui consiste em abrir o projeto a partir desta pasta e compilar. O `.gitignore` já cuidará para que os gigabytes de arquivos temporários de síntese gerados por essas IDEs fiquem de fora do GitHub.
*   **`schematics/` (Hardware Físico):** Espaço para os arquivos de desenho de circuito da protoboard. Quem estiver desenhando as conexões dos circuitos integrados deve salvar o arquivo original do software de CAD nesta pasta.

---

## ⚠️ Limitações de Armazenamento (Operação Sem Git LFS)

Para simplificar o fluxo de trabalho inicial, **não estamos utilizando o Git LFS (Large File Storage)**. Isso significa que o Git tradicional tratará qualquer arquivo não textual (imagens, PDFs, binários) como um bloco único. 

Se alterarmos um arquivo PDF de 5 MB e subirmos novamente, o Git salvará a versão antiga e a nova inteiras no histórico, fazendo o tamanho do repositório dobrar rapidamente.

Para evitar que o repositório fique lento ou atinja o limite do GitHub, devemos seguir rigorosamente as seguintes diretrizes:

1.  **Não suba Datasheets:** Nunca adicione arquivos PDF de manuais de placas de desenvolvimento ou folhas de dados de circuitos integrados (datasheets) ao repositório. Em vez disso, adicione apenas os links diretos para os documentos dos fabricantes em uma seção de referências ou dentro de um arquivo de texto.
2.  **Otimização de Imagens e Diagramas:** Ao salvar diagramas de blocos ou capturas de tela dos esquemáticos, utilize formatos comprimidos como `.png` ou `.jpg` de resolução moderada. Evite formatos pesados e sem compressão (como `.bmp`). Tente manter qualquer imagem abaixo de **1 MB**.
3.  **PDFs de Esquemáticos:** Quando a equipe da protoboard exportar o circuito em formato PDF para visualização rápida, utilize a menor resolução possível que ainda permita a leitura clara dos pinos.
4.  **Proibido Forçar o Commit de Binários:** O arquivo `.gitignore` está configurado para barrar arquivos de programação física (como `.sof` da Altera ou `.bit` da Xilinx). **Nunca utilize o comando `git add -f`** para forçar o envio desses arquivos ou de logs de simulação pesados. Eles devem ser mantidos apenas localmente na máquina de quem está programando a placa.