# LFA-Agente-Especialista
Repositório referente ao Sistema Especialista em Solos

# 🌱 Agente Especialista em Solos

Sistema especialista baseado em regras desenvolvido em Python para apoiar técnicos e engenheiros agrônomos na interpretação de laudos de análise química de solo e definição de diretrizes iniciais de manejo.

---

## 📖 Sobre o Estudo dos Solos

O estudo dos solos analisa sua formação, composição, propriedades físicas, químicas e biológicas, além de sua capacidade de uso e comportamento em diferentes aplicações, como agricultura e engenharia. Ele envolve áreas como pedologia, edafologia e geotecnia, abrangendo classificação, fertilidade, estabilidade e métodos de investigação como sondagens e ensaios laboratoriais.

Solo é a camada que recobre a superfície terrestre. Os solos são corpos formados por meio do intemperismo químico e do intemperismo físico das rochas, sendo constituídos essencialmente por minerais, matéria orgânica, água e ar, além de pequenos animais e micro-organismos. Os componentes do solo estão dispostos em camadas chamadas de horizontes. O desenvolvimento de um perfil de solo varia consideravelmente de região para região, dependendo diretamente de aspectos como clima, disponibilidade hídrica, rocha-mãe e topografia.

---

## 🎯 Finalidade e Escopo do Projeto

A partir dos dados de um laudo laboratorial e de observações de campo, o sistema avalia a fertilidade química e a acidez do solo para indicar:

1. **Classificação de adequação para cultivo:**
   * ✅ **Adequado**
   * ⚠️ **Adequado com restrição**
   * ❌ **Inadequado** (sem correção prévia)
2. **Diretrizes de manejo recomendadas:**
   * Calagem (cálculo de necessidade de calcário corrigida pelo PRNT)
   * Gessagem (avaliação de subsuperfície de 20–40 cm)
   * Correção de Fósforo (P) e Potássio (K)
   * Manejo de Matéria Orgânica (MO)
   * Práticas de conservação do solo conforme a declividade

> **Nota:** Este sistema é uma ferramenta de apoio à decisão e **não substitui o parecer de um profissional habilitado**.

---

## 🧠 Arquitetura do Sistema Especialista

Diferente de modelos de *Machine Learning*, toda decisão deste sistema deriva de regras explícitas (`SE... ENTÃO...`), auditáveis e separadas do motor de inferência:

* **Base de Fatos:** Dicionário de entrada com parâmetros do laudo e grandezas derivadas (`SB`, `t`, `T`, `V%` e `m%`).
* **Base de Regras (`R1` a `R12`):** Condições baseadas na 5ª Aproximação (CFSEMG / Embrapa) e critérios de projeto explícitos.
* **Motor de Inferência:** Avaliação sequencial na função `interpretar()`, acumulando fatores críticos, limitantes e recomendações.
* **Módulo de Explicação:** Função `gerar_relatorio()`, que exporta um arquivo `.txt` detalhando cada regra disparada, sua condição e seu motivo.
* **Interface:** Formulário interativo executado no Google Colab.

---

## 📊 Parâmetros de Entrada

| Parâmetro | Unidade | Observação |
| :--- | :---: | :--- |
| **pH** | em água | Classificação agronômica |
| **Matéria Orgânica (MO)** | `dag/kg` | Teor orgânico |
| **Fósforo (P)** | `mg/dm³` | Extrator Mehlich-1 (interpretado conforme teor de argila) |
| **Potássio (K)** | `mg/dm³` | Extrator Mehlich-1 |
| **Ca, Mg, Al, H+Al** | `cmolc/dm³` | Cátions trocáveis e acidez potencial |
| **Argila** | `%` | Define a faixa de interpretação do fósforo |
| **Declividade** | `%` | Observação de campo |
| **V desejada ($V_2$)** | `%` | Varia conforme a cultura |
| **PRNT do calcário** | `%` | Consta na embalagem do corretivo |
| **Ca e m (20–40 cm)** | `cmolc/dm³` e `%` | *Opcional* — necessário para avaliar gessagem |

---

## 🚀 Como Executar

1. Abra o notebook (`.ipynb`) deste repositório no **Google Colab** ou em um ambiente Jupyter local.
2. Execute a célula com a lógica do motor de inferência e regras (`interpretar()` e `gerar_relatorio()`).
3. Preencha os campos do formulário interativo na segunda célula com os valores do laudo de análise de solo.
4. Execute a célula para visualizar o diagnóstico e baixar o relatório explicativo em `.txt`.

---

## ⚠️ Limitações Conhecidas

* **Abrangência Regional:** Utiliza classes de interpretação da 5ª Aproximação (Minas Gerais / Cerrado) e exige extração via **Mehlich-1** para P e K.
* **Escopo Técnico:** Não calcula doses de fertilizantes NPK, não avalia micronutrientes, enxofre, atributos biológicos, propriedades físicas detalhadas (compactação/drenagem) nem incorpora legislação ambiental (Código Florestal).

---

## 👥 Autores

* **Kaynã Barbosa de Miranda**
* **Cauã Eduardo Silva de Carvalho Mendes**

*Centro Universitário - UDF | Brasília - DF — 2026*
