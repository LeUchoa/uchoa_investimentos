# Planejador de FIIs

![MIT License](https://img.shields.io/badge/license-MIT-blue)  
![Excel 365 Compatible](https://img.shields.io/badge/Excel-365%20Compatible-green)

Ferramenta em Excel (aba única **APP**) para projetar patrimônio, renda mensal e estruturar seu mix de FIIs conforme perfil de risco.  
Sem VBA, tudo na aba “APP” e compatível com Excel 365/2021.

---

## Sumário

- [Funcionalidades](#funcionalidades)  
- [Requisitos](#requisitos)  
- [Estrutura da Planilha](#estrutura-da-planilha)  
- [Como Usar](#como-usar)  
- [Download](#download)  
- [Acessibilidade](#acessibilidade)  
- [Contribuições](#contribuições)  
- [Licença](#licença)  

---

## Funcionalidades

- **Configurações**  
  Defina sua Renda Líquida Mensal, Taxa Anual de Rendimento, Percentual de Investimento e veja o Montante Sugerido.

- **Investimento Mensal**  
  Informe Capital Inicial, Aporte Mensal, Reinvestimento de Dividendos, Período (anos), Taxas e Inflação.  
  Resultado em: Patrimônio Projetado, Patrimônio Corrigido e Rendimento Mensal.

- **Cenários de Investimento**  
  Projeções de Patrimônio e Rendimento em horizontes de 2, 5, 10, 20 e 30 anos.

- **Perfil & Aporte**  
  Selecione seu perfil (Conservador, Moderado, Agressivo) e confira o Valor a Investir/Mês.

- **Alocação em FIIs**  
  Tabela com % sugerido e R$/mês para cada tipo de FII, calculados automaticamente conforme perfil.

- **Gráfico de Rosca**  
  Visualize o mix de alocação (%) e o valor total do aporte no centro do gráfico.

---

## Requisitos

- Microsoft **Excel 365** ou **Excel 2021** (para fórmulas de matriz dinâmica: `ÍNDICE` + `ESCOLHER`).  
- Excel 2016/2019: funciona mantendo a tabela de apoio e usando `SOMASES`.

---

## Estrutura da Planilha

- **Aba única: “APP”**  
  Todas as entradas, cálculos, tabela de alocação e gráfico estão nesta aba.

- **Named Ranges**  
  - `inv_Perfil` → perfil de risco (C41)  
  - `inv_Period` → aporte mensal (C42)  
  - `inv_Period_2` → mesmo valor de aporte, usado **apenas** na caixa de texto do gráfico  
  - `perfil_TotalValor` → total de D45:D50  
  - `%Alocação` → C45:C50  

---

## Como Usar

1. **Configurações**  
   - Preencha: Renda Líquida, Taxa Anual, % de Investimento.  
   - Veja o Montante Sugerido (30 % da renda).

2. **Investimento Mensal**  
   - Insira: Capital Inicial, Frequência (Mensal), Aporte (`inv_Period`), Reinvestimento, Período (anos), Taxas e Inflação.  
   - O Excel calcula automaticamente:  
     - **Patrimônio Projetado** (`VF`)  
     - **Patrimônio Corrigido** (inflação)  
     - **Rendimento Mensal**  

3. **Cenários de Investimento**  
   - Analise projeções de patrimônio e renda em 2, 5, 10, 20 e 30 anos.

4. **Perfil & Aporte**  
   - Escolha seu `inv_Perfil` (Conservador/Moderado/Agressivo) em C41.  
   - Confira o valor que será investido por mês (C42 / `inv_Period`).

5. **Alocação em FIIs**  
   - **% Sugerido** (C45:C50): fórmula matricial  
     ```excel
     =ÍNDICE(
       ESCOLHER(
         CORRESP(inv_Perfil;{"Conservador";"Moderado";"Agressivo"};0);
         {…vetor Conservador…};
         {…vetor Moderado…};
         {…vetor Agressivo…}
       );
       CORRESP(B45;{"PAPEL";"TIJOLO";"HÍBRIDOS";"FOFs";"DESENVOLVIMENTO";"HOTELARIAS"};0)
     )
     ```
   - **R$/mês** (D45:D50):  
     ```excel
     =[@%Alocação] * inv_Period
     ```
   - **Total** (D51) deve somar exatamente o aporte mensal.

6. **Gráfico de Rosca**  
   - Selecione C45:C50 e insira um **Gráfico de Rosca**.  
   - Adicione uma **Caixa de Texto** no centro, vincule a:  
     ```excel
     =inv_Period_2
     ```  
   - Formate rótulos de dados: **Fora da Extremidade** + **Linhas de Conexão** + exiba **Porcentagem**.

---

## Download

Baixe a planilha em:  
[APP.xlsx](APP.xlsx)

---

## Acessibilidade

- Cores testadas com o [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).  
- Textos alternativos (Alt Text) inseridos em gráficos e imagens para leitores de tela.

---

## Contribuições

Pull requests e issues são muito bem-vindos! Para mudanças de grande impacto, abra uma issue antes de submeter PR.

---

## Licença

Este projeto está licenciado sob a **MIT License**. Veja [LICENSE](./LICENSE) para detalhes.  
