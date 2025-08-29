# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
  <a href="https://www.fiap.com.br/">
    <img src="img/logo-fiap.png" alt="FIAP - Faculdade de Informática e Administração Paulista" border="0" width="40%" height="40%">
  </a>
</p>

---

# 📦 Enterprise Challenge - Sprint 3
<!-- Título do projeto: curto, claro, direto. Pode destacar o problema e a tecnologia principal -->

## 👥 Grupo 26
<!-- Nome oficial do grupo, se houver. Pode usar um nome criativo também -->

## 👨‍🎓 Integrantes:
- Amanda Vieira Pires (RM565045)
- Ana Gabriela Soares Santos (RM565235)
- Bianca Nascimento de Santa Cruz Oliveira (RM561390)
- Milena Pereira dos Santos Silva (RM565464)
- Nayana Mehta Miazaki (RM565045) 

## 👩‍🏫 Professores:
### Tutor(a)  
-  Lucas Gomes Moreira
### Coordenador(a)  
- André Godoi

---

# 📜 Descrição do Projeto
## 🚀 Introdução

Dando continuidade ao projeto voltado à **manutenção preditiva em linhas de envase da indústria de bebidas**, após a segunda etapa que teve como foco a simulação de um sistema embarcado responsável pela aquisição local de dados sensoriais, inicia-se a terceira etapa. Nesta etapa, os dados captados pelos sensores serão armazenados de forma estruturada para que um algoritmo de Machine Learning busque insights valiosos para a indústria.  

<!-- Após a construção de um circuito simulado com ESP32 e sensor DHT22 no ambiente Wokwi, representando um cenário em que, variações de temperatura poderiam sinalizar diferentes estados operacionais da linha de produção — de operação normal até falhas críticas. Os dados foram classificados localmente e exportados para posterior visualização e análise gráfica, reforçando a importância do monitoramento em tempo real para a detecção precoce de anomalias.-->

Link do repositório Sprint 1: https://github.com/fiap-ia-2025/enterprise-challenge-phase03

---

## 🎯 Objetivo

- Criar três circuitos virtuais com ESP32 e sensores no Wokwi;
- Simular variações de temperatura, vibração e nível de enchimento conforme diferentes momentos de operação;
- Classificar os valores em três categorias: `NORMAL`, `ALERTA_Pre_falha` e `FALHA_CRITICA`;
- Registrar os dados via Monitor Serial;
- Exportar os dados simulados para CSV;
- Gerar uma modelagem de dados relacional;
- Criar um banco de dados;
- Treinar um algoritmos de machine learning para obter insights;
- Documentar todo o processo no GitHub com prints, código e análise.

---

## 🔧 Estrutura de Simulação

- **Plataforma de Simulação:** Wokwi
- **Microcontrolador:** ESP32 (simulado)
- **Linguagem:** C++ (com base na plataforma PlataformIO com VS Code)
- **Sensor Utilizado:**  
  - `DS18B20`: sensor de temperatura digital
  - `MPU6050`: acelerômetro e giroscópio
  - `HC-SR04`: sensor de distância ultrassônico

---

## 📌 Justificativa da Escolha do Sensor

O sensor **DS18B20** foi escolhido para este projeto, pois oferece leitura precisa de **temperatura** das máquinas e não requer calibração externa, isso garante leituras confiáveis para o monitoramento de processos de envase na indústria. <br> 

Já o sensor **MPU6050**, utilizado para medir a vibração da máquina, realiza a medição de aceleramento nos três eixos X, Y e Z, detectando a intensidade e frequência das vibrações. <br> 

Por último, o sensor **HC-SR04** para fazer a medição do nível de enchimento sem fazer contato com o produto. Ele fica posicionado acima do recipiente, emite uma onda sonora e realiza a medição do tempo que o eco leva para retornar, e assim calcula-se a distância até a superfície do líquido. <br>

Nesse contexto de linhas de envase de cervejas e refrigerantes, os sensores citados acima, permitem simular as possíveis falhas durante o processo. As indústrias de bebidas enfrentam desafios frequentemente, que podem estar associados a pequenas variações na temperatura, vibração ou quantidade de líquido inserido nos produtos, que ao passar despercebidas por sistemas de monitoramentos tradicionais, podem causar interrupções significativas. Ao utilizar os sensores podemos recriar e analizar cenários onde essas condições impactam diretamente na linha de produção, para então desenvolver e testar soluções de predição e automação, capazes de identificar as anomalias e evitar falhas críticas, otimizando as operações nas linhas de envase de cervejas e refrigerantes.

---

## 🔌 Esquema dos Circuitos

## 💨 MPU5060
![Circuito MPU5060](img/mpu5060.JPG)

---

### 🧾 Trecho Representativo do Código MPU6050

O trecho abaixo representa a lógica principal do projeto, responsável por:

- Simular a leitura de vibração com base na aceleração detectada na máquina;
- Classificar o status do sistema em três níveis: `NORMAL`, `ALERTA_Pre_falha` ou `FALHA_CRITICA`;
- Exibir os dados simulados no Monitor Serial em formato CSV (separado por vírgulas), facilitando análise posterior ou exportação.

```cpp
// Trecho representativo da leitura e visualização dos dados do MPU5060

// Definição dos limites para classificação em NORMAL, ALERTA_Pre_falha ou FALHA_CRITICA
const double LIMITE_ALERTA = 16500.0; 
const double LIMITE_FALHA = 25000.0;

// Exibe os dados formatados no Monitor Serial
Serial.print(contador + 1);
Serial.print(",");
Serial.print(accTotal);
Serial.print(",");

// Classificação do status no Monitor Serial
if (accTotal < LIMITE_ALERTA) {
  Serial.println("NORMAL");
} else if (accTotal < LIMITE_FALHA) {
  Serial.println("ALERTA_Pre_falha");
} else {
  Serial.println("FALHA_CRITICA");
}

```
---

### ⚙️ Funcionamento do Sistema MPU6050

1. O ESP32 simulado lê a aceleração da máquina a cada 1 segundo através do MPU6050.
2. A vibração é simulada com valores variados, dependendo da movimentação dos eixos X, Y e Z.
3. Os dados são classificados automaticamente em três status:
   - **NORMAL**: até 16500.0LSB/g
   - **ALERTA_Pre_falha**: de 16500.0LSB/g até 25000.0LSB/g
   - **FALHA_CRITICA**: acima de 25000.0LSB/g
4. Os dados são exibidos no **Monitor Serial** no formato CSV:  
   `ID, Aceleracao_Total, Status`

---

### 🔌 Simulação no Wokwi - MPU5060 e ESP32
![Simulação MPU6050](img/mpu5060_terminal.JPG)

---

### 🧪 Exemplo de Dados Coletados MPU6050

| ID | Aceleracao_Total| Status          |
|----------|----------------|------------------|
| 32   | 5049.47           | NORMAL           |
| 97    | 18426.64         | ALERTA_Pre_falha |
| 213    | 52453.14         | FALHA_CRITICA    |

---

### 📊 Gráfico Gerado MPU5060

![Gráfico de Vibração](img/grafico_mpu5060.png)

### 📝 Estrutura e Racional do Gráfico MPU5060

O gráfico gerado apresenta a variação da aceleração simulada ao longo das medições, com o eixo X representando as medições (totalizando 500 medições) e o eixo Y representando a vibração em LSB/g (Least Significant Bit por g). Para facilitar a interpretação, a classificação foi colorida conforme **classificação automática do status operacional**:

- **NORMAL (verde)**: Aceleração abaixo de 16500.0LSB/g - operação dentro do esperado.
- **ALERTA_Pre_falha (laranja)**: Aceleração de 16500.0LSB/g até 25000.0LSB/g - possível acerelação demasiada, atenção recomendada.
- **FALHA_CRITICA (vermelho)**: Aceleração acima de 25000.0LSB/g - – indicativo de falha crítica, requer ação imediata.

---

## 🌡️ DS18B20
![Circuito DS18B20](img/DS18B20.JPG)

### 🧾 Trecho Representativo do Código DS18B20

O trecho abaixo representa a lógica principal do projeto, responsável por:

- Simular a leitura de temperatura de bebidas geladas com envase a frio;
- Classificar o status do sistema em três níveis: `NORMAL`, `ALERTA_Pre_falha` ou `FALHA_CRITICA`;
- Exibir os dados simulados no Monitor Serial em formato CSV (separado por vírgulas), facilitando análise posterior ou exportação.

```cpp
// Trecho representativo da leitura e visualização dos dados do DS18B20

// Definição dos limites para classificação em NORMAL, ALERTA_Pre_falha ou FALHA_CRITICA
const float TEMPERATURA_NORMAL_MIN = -1.0;
const float TEMPERATURA_NORMAL_MAX = 6.0;
const float TEMPERATURA_FALHA_CRITICA_MIN = -6.0;
const float TEMPERATURA_FALHA_CRITICA_MAX = 10.0;

// Exibe os dados formatados no Monitor Serial
Serial.print(contador + 1);
Serial.print(",");
Serial.print(temperatura);
Serial.print(",");

// Classificação do status no Monitor Serial
if (temperatura >= TEMPERATURA_NORMAL_MIN && temperatura <= TEMPERATURA_NORMAL_MAX) {
  Serial.println("NORMAL");
} else if (temperatura < TEMPERATURA_NORMAL_MIN || temperatura > TEMPERATURA_NORMAL_MAX) 
      
  if (temperatura >= TEMPERATURA_FALHA_CRITICA_MIN && temperatura <= TEMPERATURA_FALHA_CRITICA_MAX) {
      Serial.println("ALERTA_Pre_falha");
  } else {
      Serial.println("FALHA_CRITICA");
      }

```
---

### ⚙️ Funcionamento do Sistema DS18B20

1. O ESP32 simulado lê a temperatura da máquina a cada 1 segundo através do DS18B20.
2. A temperatura é simulada com valores variados, conforme a oscilação.
3. Os dados são classificados automaticamente em três status:
   - **NORMAL**: até 6ºC
   - **ALERTA_Pre_falha**: de 6ºC até 10ºC
   - **FALHA_CRITICA**: acima de 10ºC
4. Os dados são exibidos no **Monitor Serial** no formato CSV:  
   `ID, Temperatura, Status`

---

### 🔌 Simulação no Wokwi - DS18B20 e ESP32
![Simulação DS18B20](img/ds18b20_terminal.JPG)


### 🧪 Exemplo de Dados Coletados DS18B20

| ID | Temperatura | Status          |
|----------|----------------|------------------|
| 17   | 1.37          | NORMAL           |
| 65   | 8.38         | ALERTA_Pre_falha |
| 118   | 14.25         | FALHA_CRITICA    |

### 📊 Gráfico Gerado DS18B20

![Gráfico de Temperatura](img/grafico_DS18B20.png)

### 📝 Estrutura e Racional do Gráfico DS18B20

O gráfico gerado apresenta a variação da temnperatura simulada ao longo das medições (totalizando 500 medições). Para facilitar a interpretação, a classificação foi colorida conforme **classificação automática do status operacional**:

- **NORMAL (verde)**: Temperatura abaixo de 6ºC - operação dentro do esperado.
- **ALERTA_Pre_falha (laranja)**: Temmperatura de 6ºC até 10ºC - possível acerelação demasiada, atenção recomendada.
- **FALHA_CRITICA (vermelho)**: Temperatura acima de 10ºC - – indicativo de falha crítica, requer ação imediata.


## 〰️ HC-SR04
![Circuito HC-SR04](img/HC-SR04.JPG)


### 🧾 Trecho Representativo do Código HC-SR04

O trecho abaixo representa a lógica principal do projeto, responsável por:

- Simular a leitura de nível de enchimento dos recipientes de bebidas;
- Classificar o status do sistema em três níveis: `NORMAL`, `ALERTA_Pre_falha` ou `FALHA_CRITICA`;
- Exibir os dados simulados no Monitor Serial em formato CSV (separado por vírgulas), facilitando análise posterior ou exportação.

```cpp
// Trecho representativo da leitura e visualização dos dados do HC-SR04

// Definição dos limites para classificação em NORMAL, ALERTA_Pre_falha ou FALHA_CRITICA
const float ALTURA_MAXIMA = 20.0;
const float NIVEL_NORMAL_MIN = 19.0;
const float NIVEL_NORMAL_MAX = 20.0;
const float NIVEL_ALERTA_MIN = 16.0;
const float NIVEL_ALERTA_MAX = 19.0;

// Exibe os dados formatados no Monitor Serial
 Serial.print(contador + 1);
    Serial.print(",");
    Serial.print(distancia_cm);
    Serial.print(",");
    Serial.print(nivel_cm);
    Serial.print(",");

 // Classificação do status no Monitor Serial   
    if (nivel_cm >= NIVEL_NORMAL_MIN && nivel_cm <= NIVEL_NORMAL_MAX) {
      Serial.println("NORMAL");
    } else if (nivel_cm >= NIVEL_ALERTA_MIN && nivel_cm < NIVEL_NORMAL_MIN) {
      Serial.println("ALERTA_Pre_falha");
    } else {
      Serial.println("FALHA_CRITICA");
    }

```

---

### ⚙️ Funcionamento do Sistema HC-SR04

1. O ESP32 simulado lê a distância do líquido até o sensor HC-SR04 a cada 1 segundo.
2. A temperatura é simulada com valores variados, conforme a oscilação.
3. Os dados são classificados automaticamente em três status:
   - **NORMAL**: de 19 a 20cm
   - **ALERTA_Pre_falha**: de 16 a 18cm
   - **FALHA_CRITICA**: abaixo de 16cm
4. Os dados são exibidos no **Monitor Serial** no formato CSV:  
   `ID, Distancia_cm, Nivel_cm, Status`

---

### 🔌 Simulação no Wokwi - HC-SR04 e ESP32
![Simulação HC-SR04](img/HC-SR04_terminal.JPG)

### 🧪 Exemplo de Dados Coletados HC-SR04

| ID | Distancia_cm | Nivel_cm         | Status          |
|----|--------------|------------------|-----------------|
| 29 | 1.94         | 23.06            | NORMAL          |
| 99 | 7.97         | 17.03            | ALERTA_Pre_falha|
| 213| 9.07         | 15.93            | FALHA_CRITICA   |

### 📊 Gráfico Gerado HC-SR04

![Gráfico de Nível de Enchimento](img/grafico_HC-SR04.png)

### 📝 Estrutura e Racional do Gráfico HC-SR04

O gráfico gerado apresenta a variação do nível de enchimentos dos recipientes simulado ao longo das medições (totalizando 500 medições). Para facilitar a interpretação, a classificação foi colorida conforme **classificação automática do status operacional**:

- **NORMAL (verde)**: Nível de 19 a 20cm - operação dentro do esperado.
- **ALERTA_Pre_falha (laranja)**: Nível de 16 a 18cm - possível acerelação demasiada, atenção recomendada.
- **FALHA_CRITICA (vermelho)**: Nível abaixo de 16cm - – indicativo de falha crítica, requer ação imediata.

---

## ✅ Insights Iniciais

- **NORMAL**
- **ALERTA_Pre_falha**
- **FALHA_CRITICA**

Essa análise demonstra que o sistema de simulação e classificação está funcionando conforme esperado, permitindo a identificação clara de mudanças na vibração, temperatura e nível de enchimento. Isso é essencial para o monitoramento preventivo e tomada de decisão.

Essa categorização tem como objetivo simular o comportamento de um sistema embarcado que não apenas coleta dados, mas também realiza uma **análise embarcada**, classificando os dados com base em faixas de operação seguras ou críticas. Essa estratégia permite que o dispositivo reaja localmente ou envie alertas para a nuvem em casos de falha iminente, antecipando paradas e aumentando a confiabilidade do processo industrial.

Os gráficos apresentados anteriormente, também fornecem uma visão clara da transição entre os diferentes estados, evidenciando o momento em que o sistema passa de uma operação estável para condições críticas.

---

# 🔍 Entidades e Atributos
![Fluxograma de Entidades e Atributos](img/entidades-atributos.jpg)

## MAQUINAS

- id_maquina
- nome (maquina_1, maquina_2, maquina_3)
- localizacao (area_1, area_2)

## SENSORES

- id_sensor
- id_maquina
- tipologia (temperatura, vibracao, nivel_enchimento)

## MEDICAO VIBRACAO

- id
- id_sensor
- medicao (resultado da medição do sensor)
- status (NORMAL, ALERTA_Pre_falha, FALHA_CRITICA)

## MEDICAO TEMPERATURA

- id
- id_sensor
- medicao (resultado da medição do sensor)
- status (NORMAL, ALERTA_Pre_falha, FALHA_CRITICA)

## MEDICAO NIVEL DE ENCHIMENTO

- id
- id_sensor
- medicao (resultado da medição do sensor)
- status (NORMAL, ALERTA_Pre_falha, FALHA_CRITICA)

# 🔗 Relacionamentos (Cardinalidades)

| Entidade 1 | Relacionamento | Entidade 2    | Cardinalidade | Observação                                            |
|------------|----------------|---------------|---------------|-------------------------------------------------------|
| Maquinas   | possui         | Sensores      | 1:N           | Uma máquina pode possuir vários sensores               |
| Sensores   | faz            | Medicao Vibração      | 1:N           | Um sensor podem fazer várias medições de vibração|
| Sensores   | faz            | Medicao Temperatura      | 1:N           | Um sensor podem fazer várias medições de temperatura|
| Sensores   | faz            | Medicao Nível de enchimento    | 1:N           | Um sensor podem fazer várias medições de nível|

---

# 🗝️ Modelagem de dados
![Modelagem de dados](img/modelagem.JPG)

> Para a modelagem dos dados foi utilizado o site dbdiagram.io

```cpp
// Trecho representativo da criação da modelagem de dados

TABLE MEDICAO_VIBRACAO { // Criação da tabela definindo as colunas e suas características e restrições
  id INT [primary key]
  id_sensor INT
  aceleracao_total FLOAT
  status VARCHAR(20)
  }

Ref: "SENSORES"."id_sensor" < "MEDICAO_VIBRACAO"."id_sensor" // Referenciando a chave estrangeira com outra coluna

```

![Código para Modelagem de dados](img/codigo_modelagem.JPG)

---

# 📊 Banco de dados

```cpp
// Trecho representativo da criação do banco de dados
// Primeiro importar o arquivo .csv gerado pela medição sensor correspondente

ALTER TABLE medicao_vibracao ADD COLUMN id_sensor; // adicionar a coluna id_sensor

UPDATE medicao_vibracao SET id_sensor = 3; // informar que o sensor tem o id '3' da tabela SENSORES

ALTER TABLE medicao_vibracao RENAME TO medicao_vibracao_old; // Alterar o nome da tabela para criar uma nova com a chave estrangeira id_sensor

CREATE TABLE MEDICAO_VIBRACAO ( //Criação da nova tabela
  id INT PRIMARY KEY,
  id_sensor INT,
  aceleracao_total FLOAT,
  status VARCHAR(20),
  FOREIGN KEY (id_sensor) REFERENCES SENSORES(id_sensor)
  );
 
 INSERT INTO MEDICAO_VIBRACAO (id, id_sensor, aceleracao_total, status) //Adição dos dados contidos na tabela anterior
 SELECT ID, id_sensor, Aceleracao_Total, Status
 FROM medicao_vibracao_old;
 
 DROP TABLE medicao_vibracao_old; // Deletar tabela antiga
  
```

---

# 📜 Etapas

## 1. Cadastro de máquinas
Há necessidade de cadastrar todas as máquinas da indústria.

📊 **Dados Necessários**
- Nome da máquina
- Localização da máquina dentro da indústria

## 2. Identificação dos sensores
Há necessidade de identificação de todos os sensores presentes nas máquinas.

📊 **Dados Necessários**
- Tipologia
- Máquina localizada

## 3. Recebimento de dados de sensores
O sistema deverá receber os dados de cada sensor.

📊 **Dados Recebidos**
- Medição
- Status

## 4. Banco de dados
A partir das informações recebidas e registradas, deverão ser armazenadas em um banco de dados. 

> Os relacionamentos entre as entidades irão proporcionar insights valiosos que poderão ser detectados pelo modelo preditivo.

---

# 🖥️ Machine Learning


## 📁 Estrutura do Repositório

```bash
/enterprise-challenge-phase04
├── src/
│   ├──main.cpp
│
├── diagram.json                # Circuito simulado no Wokwi
├── platformio.ini              # Configuração do PlatformIO
├── wokwi.toml                  # Caminho para firmware na simulação
├── dados_temperatura.csv       # Registro dos dados
├── grafico.ipynb               # Gráfico de temperatura simulada
│ 
├── img/                        # Imagens utilizadas no README
│   ├── circuito.png            # Print do circuito no Wokwi
│   ├── logo_fiap.png           # Logo da faculdade
│   ├── grafico.png             # Imagem do gráfico
│   ├── simulacao.png           # Imagem da simulação no Wokwi
       
│
├── .gitignore                  # Arquivos/pastas ignorados pelo Git
└── README.md                   # Documentação geral do projeto
```
---

## 🧠 Conclusão

---

## 📜 Licença

Este projeto está licenciado sob os termos da licença **CC BY 4.0**.

---
