Chatbot to help diabetic people
# Chatbot Médico Inteligente com Google Gemini 

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![Google Gemini](https://img.shields.io/badge/Google%20Gemini-API-green.svg)](https://ai.google.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Este projeto demonstra a criação de um chatbot interativo utilizando a API Google Gemini para auxiliar usuários a entenderem suas receitas médicas. O chatbot é capaz de processar documentos PDF (receitas), extrair informações sobre medicamentos e insumos, e fornecer uma **estimativa de custos simulada** com base em consultas (simuladas) a três grandes redes de farmácias brasileiras.

## ✨ Visão Geral

Muitas vezes, pacientes recebem prescrições médicas complexas e têm dificuldade em entender todos os itens ou estimar os custos envolvidos no tratamento. Este chatbot visa:

*   Analisar receitas médicas em formato PDF.
*   Extrair uma lista de medicamentos, insumos e equipamentos.
*   Fornecer uma estimativa de custo **simulada** para os itens da receita, consultando (de forma simulada) preços nas farmácias Drogasil, Droga Raia e Drogaria São Paulo.
*   Oferecer cálculos auxiliares para pacientes com diabetes (ex: dose de insulina baseada em contagem de carboidratos).
*   Operar com foco na segurança, sempre alertando que as informações não substituem o aconselhamento médico profissional.

## 🚀 Funcionalidades Principais

*   **Upload de Receitas PDF:** Usuários podem carregar suas receitas médicas.
*   **Extração Inteligente de Itens:** O Google Gemini analisa o PDF e extrai:
    *   Nome do medicamento/insumo/equipamento.
    *   Apresentação/Dosagem.
    *   Quantidade descrita.
    *   Tipo de item (medicamento, insumo, equipamento).
*   **Estimativa de Custos (SIMULADA):**
    *   Para cada item extraído, o sistema "consulta" (simuladamente) os preços nas farmácias alvo.
    *   Calcula o custo total estimado para cada item com base na quantidade da receita e no preço da embalagem.
    *   Apresenta uma faixa de custo total para a receita.
    *   **Aviso:** Esta funcionalidade é puramente demonstrativa com preços fictícios.
*   **Assistente para Diabetes:** Ajuda com cálculos de insulina se os parâmetros forem fornecidos.
*   **Interface Conversacional:** Interação via chat em um notebook Google Colab.

## 🛠️ Como Funciona (Tecnologias)

*   **Backend (Lógica):** Python executado em um notebook Google Colab.
*   **Inteligência Artificial:**
    *   **Google Gemini API (modelo `gemini-1.5-flash-latest` ou similar):** Para processamento de linguagem natural, análise de documentos PDF (multimodalidade) e extração de informações estruturadas (JSON).
*   **Simulação de Consulta de Preços:**
    *   O código Python contém funções que *simulam* a busca de preços nas farmácias. **Não há web scraping real neste protótipo.**
*   **Interface:** Interação direta no notebook Google Colab.

## 📋 Pré-requisitos

*   Uma conta Google.
*   Acesso à API Google Gemini (você precisará de uma **API Key**). Você pode obtê-la no [Google AI Studio](https://aistudio.google.com/app/apikey).
*   Familiaridade básica com Google Colab e Python.

## ⚙️ Configuração e Execução

1.  **Clone o Repositório (ou baixe o arquivo `.ipynb`):**
    ```bash
    # Se você clonar:
    # git clone https://github.com/SEU_USUARIO/NOME_DO_SEU_REPOSITORIO.git
    # cd NOME_DO_SEU_REPOSITORIO
    ```
2.  **Abra no Google Colab:**
    *   Faça o upload do arquivo `Alura_Python_Imersao (3).ipynb` (ou o nome que você deu) para o seu Google Drive e abra-o com o Colab, ou vá em "Arquivo" -> "Upload notebook" no Colab.
3.  **Instale as Dependências:**
    *   Execute a primeira célula de código do notebook para instalar as bibliotecas necessárias:
      ```python
      # CELL 1: Install Google Gemini SDK and necessary libraries...
      !pip install google-genai google-generativeai requests beautifulsoup4 lxml
      ```
4.  **Configure sua API Key do Gemini:**
    *   No painel esquerdo do Colab, clique no ícone de chave ("Secrets").
    *   Adicione um novo secret com o nome `GOOGLE_API_KEY`.
    *   Cole sua chave da API Gemini no campo "Value".
    *   Certifique-se de que a opção "Notebook access" está habilitada para este secret.
5.  **Execute as Células:**
    *   Execute as células do notebook em ordem, uma por uma, ou use "Ambiente de execução" -> "Executar tudo".
    *   A Célula 6 (Configuração do Chatbot) e a Célula 7 (Funções Auxiliares) precisam ser executadas antes da Célula 8 (Loop Interativo).

## 💬 Como Usar o Chatbot

Após executar todas as células de configuração (até a Célula 8, que contém o loop `while True`):

1.  **Início:** O chatbot saudará você e estará pronto para interagir no campo de entrada que aparece abaixo da célula em execução.
2.  **Fazer Upload de uma Receita:**
    *   Digite `upload` ou `carregar arquivo` e pressione Enter.
    *   Uma caixa de diálogo de upload de arquivo do Colab aparecerá. Selecione o arquivo PDF da sua receita.
    *   O chatbot processará o arquivo e tentará extrair a lista de itens.
3.  **Perguntar sobre a Receita:**
    *   Ex: `Quais medicamentos estão na receita?`
    *   Ex: `Qual a posologia da Insulina Fiasp?`
4.  **Pedir Estimativa de Custos:**
    *   Após o upload e extração bem-sucedidos, digite: `Qual o custo estimado dos itens da receita?` ou `preço dos medicamentos`.
    *   O chatbot apresentará uma estimativa **simulada** e os devidos avisos.
5.  **Cálculos para Diabetes:**
    *   Ex: `Quanto de insulina para 50g de carboidratos?` (O chatbot pedirá seus parâmetros se não os encontrar na receita).
6.  **Sair:** Digite `fim` para encerrar a sessão do chat.

## ⚠️ Considerações Importantes e Limitações

*   **NÃO É ACONSELHAMENTO MÉDICO:** Este chatbot é uma ferramenta experimental e informativa. **As informações fornecidas NÃO substituem, de forma alguma, o aconselhamento de um médico ou profissional de saúde qualificado.** Sempre consulte seu médico para decisões sobre seu tratamento.
*   **ESTIMATIVAS DE PREÇO SÃO SIMULADAS:** A funcionalidade de estimativa de custos neste protótipo utiliza **preços fictícios e uma lógica de busca simulada**. Os valores apresentados **NÃO SÃO REAIS** e não devem ser usados para decisões financeiras. Para preços reais, consulte diretamente as farmácias.
*   **PRECISÃO DA EXTRAÇÃO DO PDF:** A capacidade do Gemini de extrair informações de PDFs é poderosa, mas pode variar dependendo da qualidade, formato e clareza do PDF. Receitas manuscritas ou com layouts muito complexos podem ser desafiadoras.
*   **PRIVACIDADE:** Ao fazer upload de um documento, ele é enviado para a API do Google para processamento. Esteja ciente das políticas de privacidade e uso de dados do Google Gemini. Para informações médicas sensíveis, considere as implicações.
*   **WEB SCRAPING REAL:** Para obter preços reais, seria necessário implementar uma solução robusta de web scraping para os sites das farmácias, o que é complexo, requer manutenção constante e pode estar sujeito aos termos de serviço dos sites.
*   **MELHORIAS FUTURAS:** Este é um protótipo. Muitas melhorias podem ser feitas, como a implementação de scraping real, uma interface de usuário mais amigável, e maior robustez na interpretação de diferentes formatos de receita.

## 🚀 Melhorias Futuras (Sugestões)

*   **Implementação de Web Scraping Real:** Substituir a simulação de preços por scraping real dos sites das farmácias alvo.
*   **Interface Gráfica do Usuário (GUI):** Desenvolver uma interface web (ex: com Flask/FastAPI + HTML/JS) ou um aplicativo para facilitar o uso.
*   **Cache de Preços:** Para a versão com scraping real, implementar um cache para evitar consultas repetidas e reduzir a carga nos sites.
*   **Suporte a Mais Farmácias:** Expandir a consulta de preços para outras redes.
*   **Tratamento de Erros Aprimorado:** Melhorar a forma como o chatbot lida com falhas na extração ou na busca de preços.
*   **Personalização:** Permitir que o usuário informe seu CEP para tentar buscar preços mais localizados (se os sites das farmácias suportarem isso facilmente).
*   **Internacionalização:** Adaptar para outros idiomas e sistemas de saúde.

## 🤝 Contribuições

Contribuições são bem-vindas! Se você tiver ideias para melhorias ou encontrar bugs, sinta-se à vontade para abrir uma *issue* ou um *pull request*.

## 📜 Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE).

## 🙏 Agradecimentos

*   À [Alura](https://www.alura.com.br/) pelos cursos e imersões que inspiram projetos como este.
*   Ao time do [Google Gemini](https://ai.google.dev/) por disponibilizar uma API de IA tão poderosa.
