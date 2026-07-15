# Controle

Projeto em Arduino (C++) para modelagem e controle de velocidade de um motor DC com encoder, usando uma ponte H e um controlador PID.

O repositório reúne os sketches desenvolvidos durante um trabalho de identificação de sistemas e controle: primeiro a etapa de **modelagem** (levantamento da resposta do motor em malha aberta) e depois a etapa de **controle PID** (malha fechada, com setpoint ajustável via monitor serial).

## Como funciona

- Um **encoder** ligado à interrupção do pino 2 conta pulsos a cada rotação do eixo do motor.
- A cada 1 segundo, o firmware calcula a velocidade angular (rad/s) a partir do número de pulsos contados.
- Um **controlador PID** (proporcional, integral, derivativo) compara a velocidade medida com um *setpoint* e ajusta o sinal PWM enviado ao motor por uma ponte H, para manter a velocidade desejada.
- O *setpoint* pode ser alterado em tempo real digitando um novo valor no Monitor Serial (9600 baud).

## Estrutura do repositório

| Arquivo | Descrição |
|---|---|
| `controlemodelagem.ino` | Etapa de modelagem: motor rodando em malha aberta (PWM fixo) para levantar a curva de resposta do sistema. |
| `controlemotorpid_cal.ino` | Controlador PID calibrado, em malha fechada, com leitura do setpoint via Serial. |
| `trabcontrolmodel.ino` | Versão do trabalho de controle e modelagem. |
| `sketch_aug19b.ino`, `sketch_sep29a.ino`, `sketch_dec13a.ino`, `sketch_dec13a_copy_20241213194140.ino`, `sketch_nov27a_copy_20241212194253.ino`, `sketch_jul27a.ino` | Sketches intermediários/experimentais gerados ao longo do desenvolvimento. |
| `.gitignore`, `.gitattributes` | Arquivos de configuração do Git. |

## Hardware utilizado

- Arduino (Uno ou compatível)
- Motor DC com encoder incremental
- Ponte H (driver de motor) — pino de *enable* no pino 8
- Motor ligado às saídas PWM (pinos 5/6/9, dependendo do sketch)
- Encoder ligado ao pino 2 (interrupção externa)

> Os valores de ganho `kp`, `ki` e `kd`, o número de pulsos por volta e os pinos usados variam entre os sketches — confira o arquivo específico antes de gravar no seu hardware, pois foram ajustados para a bancada de testes.

## Como usar

1. Abra o sketch desejado (`controlemodelagem.ino` para malha aberta ou `controlemotorpid_cal.ino` para controle PID) na IDE do Arduino.
2. Confira a ligação dos pinos do motor, do encoder e do *enable* da ponte H, ajustando as constantes no início do código se necessário.
3. Faça o upload para a placa.
4. Abra o Monitor Serial a 9600 baud para acompanhar a velocidade medida.
5. No sketch de controle PID, digite um número no Monitor Serial e envie para definir um novo setpoint de velocidade.

## Requisitos

- [Arduino IDE](https://www.arduino.cc/en/software) (ou PlatformIO)
- Placa Arduino compatível com interrupções externas (Uno, Nano, Mega etc.)

## Status

Projeto acadêmico/experimental, sem releases publicadas. Os diversos sketches representam iterações do desenvolvimento e podem conter trechos comentados usados durante os testes.

