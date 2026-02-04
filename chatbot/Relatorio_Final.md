# Relatório Final: Chatbot de Apoio Institucional com RAG

**Projeto:** Chatbot de Apoio baseado no ICVS Onboarding Manual  
**Unidade Curricular:** Introdução à Inteligência Artificial  
**Ano letivo:** 2025/2026  
**Autores:** Grupo 10 (Ana Maciel, Eduarda Veloso, João Garção e Michel Gonçalves)

## 1. Problema Escolhido e Motivação

O problema abordado foi a criação de um chatbot informativo para auxiliar novos estudantes, investigadores e colaboradores do Instituto de Investigação em Ciências da Vida e da Saúde (ICVS) durante o processo de onboarding. O chatbot deve responder a perguntas sobre procedimentos administrativos, estruturas internas, normas e recursos disponíveis, baseando-se exclusivamente no manual institucional para garantir precisão e confiabilidade.

**Motivação:**  
Reduzir a dependência de consultas manuais ao documento, oferecendo suporte 24/7 e melhorando a experiência de integração. Demonstra aplicações práticas de IA em contextos institucionais, promovendo eficiência e acessibilidade.

## 2. Dataset/Documentos/Textos Utilizados e Respetiva Preparação

**Dataset Principal:** ICVS Onboarding Manual (formato .docx convertido para .txt).  
**Preparação:**  
- **Etapa I:** Conversão para CSV estruturado (197 entradas por parágrafo). Limpeza (minúsculas, remoção de pontuação/números), tokenização, lematização e remoção de stopwords com NLTK. Representação vetorial via TF-IDF (1000 features).  
- **Etapa II:** Enriquecimento com spaCy (NER para entidades) e TF-IDF (palavras-chave), gerando JSON com metadados semânticos.  
- **Etapa III:** Uso direto do CSV para recuperação, com testes de integração JSON.

**Justificação:** Estrutura granular preserva contexto; limpeza assegura qualidade vetorial.

## 3. Tecnologias Escolhidas e Justificação da Escolha

**Tecnologias Principais:**  
- **Pré-processamento:** Pandas, NLTK, scikit-learn (TF-IDF).  
- **Extração:** spaCy (NER).  
- **Geração:** Ollama com Phi (modelo leve).  
- **Interface:** Python CLI.

**Por que razão esta abordagem?**  
RAG combina recuperação factual (TF-IDF) com geração natural (LLM), evitando alucinações e garantindo respostas contextuais. Modularidade permite iteração e manutenção.

**Alternativas Consideradas:**  
- Uso exclusivo de LLM (ex.: GPT) sem recuperação—rejeitado por risco de alucinações e falta de controle factual.  
- Outros modelos (Llama3.1:8b)—descartado por requisitos de RAM.  
- Interfaces web (ex.: Streamlit)—simples CLI priorizada para foco em core.

## 4. Arquitetura Implementada

- **Etapa I:** Pipeline de pré-processamento → Dataset limpo + TF-IDF.  
- **Etapa II:** Extração de conhecimento → JSON enriquecido.  
- **Etapa III:** Sistema RAG (recuperação TF-IDF + geração Ollama) + CLI modular (`retrieval.py`, `RAG.py`, `config.py`, `fim.py`).  
- Fluxo: Pergunta → Recuperação top-k → Contexto → Geração resposta.

## 5. Demonstração dos Resultados

Exemplos de perguntas e respostas (CLI com Phi):

1. **Pergunta:** Quem devo contatar para treinamento de segurança?  
   **Resposta:** Com base nas nossas informações, você pode contatar training.icvs@med.uminho.pt para questões de treinamento ou safety.icvs@med.uminho.pt para dúvidas gerais de segurança. Evidências: Access to Specialized Facilities, Mandatory Safety Training.

2. **Pergunta:** O que preciso fazer para obter o cartão ICVS?  
   **Resposta:** Para obter o cartão ICVS, preencha o formulário de onboarding e agende uma foto institucional. O IT processará o cartão. Evidências: Administrative and Technical Units, ICVS Identification Card.

3. **Pergunta:** Como solicitar acesso à instalação de microscopia?  
   **Resposta:** Identifique necessidades, indique no formulário de onboarding, complete treinamento específico, demonstre competência e assine documentação. Evidências: Access to Specialized Facilities.

4. **Pergunta:** Quais são os princípios fundamentais da integridade na pesquisa?  
   **Resposta:** Os princípios incluem honestidade, responsabilidade e transparência. Evidências: Fundamental Principles.

## 6. Discussão Crítica

**O que funciona bem?**  
- Respostas precisas e conversacionais para perguntas diretas; recuperação eficiente com TF-IDF; modularidade facilita ajustes.

**Limitações?**  
- Alucinações em perguntas vagas/complexas; dependência de qualidade do dataset; modelos leves limitam nuance; não lida com multi-turnos.

**Comparação breve com método alternativo:**  
Se usássemos LLM puro (ex.: GPT sem RAG), respostas seriam mais fluidas mas propensas a invenções externas, perdendo precisão institucional. RAG adiciona controle factual, ideal para domínios específicos.

## 7. Conclusões e Trabalho Futuro

O projeto entregou um chatbot RAG funcional, demonstrando viabilidade de IA para suporte institucional. Resultados positivos em precisão e usabilidade.

**Trabalho Futuro:**  
- Integração com modelos maiores; expansão para multi-turnos; interface web; avaliação em larga escala; otimização com vetores densos (ex.: embeddings).

Este relatório consolida as etapas, provando o potencial do RAG em aplicações práticas.</content>
<parameter name="filePath">c:\Users\gonsa\OneDrive\Microsoft Teams Chat Files\Desktop\chatbot\final_report.md