# Controle motor elétrico PMSM
Este repositório tem o estudo feito sobre controle de motores elétricos PMSM sensorless, desenvolvido na disciplina de laboratório de sinais do curso de engenharia de controle e automação.

Este trabalho foi realizado durante a disciplina de Laboratório de Controle e Sinais do curso de Engenharia de Controle e Automação do Instituto Federal Fluminense. 


## Visão Geral do Projeto
O objetivo principal deste trabalho é projetar a modelagem matemática e o controle de velocidade de um motor PMSM. A partir de parâmetros reais de um motor, foram estruturados dois cenários de simulação: um **modelo linearizado** e um **modelo não linear**. 

Para o controle, foram sintetizados controladores **PI** acoplados a uma estrutura de ganho ótimo via **LQR** (Regulador Linear Quadrático) com estados aumentados, além da integração de um **Filtro de Kalman (FK)** para estimativa de estados na presença de ruídos de processo e de medição.

## 📂 Estrutura do Repositório

*   `/data`: Contém os parâmetros construtivos e de operação do motor PMSM (resistência, indutância, inércia, fluxo magnético, etc.) utilizados para alimentar os scripts e simulações.
*   `/src`: Scripts em MATLAB (`.m`) responsáveis pelo cálculo do ponto de operação, matrizes de linearização do sistema ($A$ e $B$), análise das funções de transferência e sintese dos controladores.
*   `/project`: Arquivos e diagramas de blocos desenvolvidos no Simulink (`.slx`) que implementam a malha de controle, o inversor, a transformação de Clarke-Park ($abc/dq$) e a dinâmica do motor.
*   `/figures`: Imagens, diagramas de setup e gráficos de resposta temporal das correntes ($i_d, i_q$) e velocidade ($\omega$) gerados durante as análises.


## 🎛️ Detalhes do Sistema Dinâmico

A modelagem do motor baseia-se nas equações diferenciais da parte elétrica (eixos $d-q$) e mecânica:

$$V_d = L \frac{d(i_d)}{dt} + R \cdot i_d - N \cdot L \cdot i_q \cdot \omega$$
$$V_q = L \frac{d(i_q)}{dt} + R \cdot i_q + N \cdot L \cdot i_d \cdot \omega + \sqrt{\frac{6}{2}} N \cdot \lambda_m \cdot \omega$$
$$J \dot{\omega} + b \cdot \omega = K_t \cdot i_q$$

As simulações validam o comportamento do sistema respeitando os seguintes limites físicos do modelo:
* Velocidade Máxima ($\omega_{max}$): $250 \text{ rad/s}$ 
* Corrente Máxima ($\sqrt{i_d^2 + i_q^2}_{max}$): $3 \text{ A}$ 
* Tensão Máxima ($\sqrt{V_d^2 + V_q^2}_{max}$): $50 \text{ V}$ 


## 💻 Requisitos e Tecnologias

Os scripts foram desenvolvidos utilizando [MATLAB / Simulink].

### Toolboxes Necessárias:
* Control System Toolbox
* Simscape / Simscape Electrical (se aplicável ao seu modelo)
* Statistics and Machine Learning Toolbox
* Deep Learning Toolbox
