# Tranca Escape Room com BitDogLab

Sistema embarcado desenvolvido para controlar a abertura de uma caixa-cofre utilizada na etapa final de um **Escape Room educativo desenvolvido na XI SECITEC da UFERSA Campus Angicos**.  
O projeto foi implementado com a placa **BitDogLab**, integrando **teclado matricial**, **servo motor**, **LED RGB**, **botões físicos** e **display OLED SSD1306**, permitindo a validação de senhas e a abertura automatizada da caixa que armazenava a chave da vitória do desafio.

## Visão Geral

Este projeto foi criado para compor a lógica final de uma experiência imersiva realizada em uma atividade acadêmica e extensionista. A proposta consistiu em desenvolver uma **tranca eletrônica funcional** para uma caixa de segredo, que pudesse ser aberta apenas mediante a digitação da senha correta.

A caixa foi utilizada na **sala 4**, etapa final do Escape Room, funcionando como elemento decisivo da dinâmica. Ao resolver os enigmas e descobrir a combinação correta, os participantes digitavam a senha no teclado matricial. Se a combinação estivesse correta, o sistema acionava o servo motor, abria a caixa por alguns segundos e permitia a retirada da chave que garantia a vitória da equipe.

## Objetivo do Projeto

Desenvolver uma solução embarcada simples, funcional e portátil para automatizar a abertura de uma caixa-cofre em um Escape Room, integrando hardware e software em uma experiência interativa, imersiva e educativa.

## Principais Funcionalidades

- Leitura de senha por **teclado matricial**
- Validação de múltiplas senhas cadastradas no código
- Abertura automática da caixa com **servo motor**
- Indicação visual de status com **LED RGB**
- Exibição de mensagens e senha digitada em **display OLED**
- Confirmação e correção da senha com os **botões físicos da BitDogLab**
- Fechamento automático após tempo de abertura

## Hardware Utilizado

- **BitDogLab**
- **Servo motor**
- **Teclado matricial 4x4**
- **Display OLED SSD1306 via I2C**
- **LED RGB**
- **Botões físicos da própria placa**
- **Caixa de madeira adaptada**

## Justificativa da Escolha da BitDogLab

A **BitDogLab** foi escolhida por oferecer um conjunto de recursos que facilitaram a implementação do protótipo, como:

- alimentação por bateria;
- GPIOs disponíveis para expansão;
- interface **I2C**;
- botões físicos integrados;
- display embarcado;
- boa adequação para prototipagem e aplicações educacionais.

Embora plataformas como **Arduino** ou **ESP32** também pudessem ser utilizadas, a BitDogLab atendeu de forma satisfatória aos requisitos de portabilidade, integração e simplicidade do projeto.

## Lógica de Funcionamento

O sistema opera em três estados principais:

### 1. Estado inicial
Ao iniciar, a caixa permanece fechada.

Nesse estado:
- o servo motor permanece em posição de travamento;
- o LED RGB sinaliza o estado de atenção/operação;
- o display exibe a mensagem solicitando a digitação da senha.

### 2. Entrada da senha
A senha é digitada pelo teclado matricial.

Durante esse processo:
- os dígitos são mostrados no display OLED;
- o **botão ENTER** confirma a tentativa;
- o **botão BACK** apaga o último dígito digitado.

### 3. Validação
Após a entrada da senha, o sistema compara o valor digitado com as senhas válidas cadastradas no programa.

- Se a senha estiver **correta**:
  - o LED muda para **verde**;
  - o servo motor abre a caixa;
  - o display informa que a senha está correta;
  - a caixa permanece aberta por **20 segundos**;
  - após esse tempo, o sistema fecha novamente.

- Se a senha estiver **incorreta**:
  - o LED muda para **vermelho**;
  - a caixa permanece fechada;
  - o display informa erro;
  - após alguns segundos, o sistema retorna ao estado inicial.

## Controle Visual do Sistema

O projeto utiliza um **LED RGB** para representar os estados do sistema:

- **Verde** → caixa aberta / senha correta
- **Amarelo** → estado normal de operação
- **Vermelho** → senha incorreta / acesso negado

## Controle do Servo Motor

A tranca foi implementada com um **servo motor** acoplado à tampa da caixa.

No código atual:
- **140°** representa o estado de **caixa fechada**
- **50°** representa o estado de **caixa aberta**

Esse mecanismo permite uma abertura simples e funcional, adequada à proposta do desafio.

## Estrutura do Repositório

```text
tranca_escape_room/
├── .gitignore
├── CMakeLists.txt
├── pico_sdk_import.cmake
├── lwipopts.h
├── blink.pio
├── tranca_escape_room.c
├── inc/
│   ├── ssd1306.h
│   ├── ssd1306_font.h
│   ├── ssd1306_i2c.h
│   └── ssd1306_i2c.c
├── .vscode/
│   ├── c_cpp_properties.json
│   ├── cmake-kits.json
│   ├── extensions.json
│   ├── launch.json
│   ├── settings.json
│   └── tasks.json
└── build/
