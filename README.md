🚗🔒 Acionamento Automatizado de Cancela – Sistema LPR
TCC – Automação de Controle de Acesso com Reconhecimento de Placas
<div align="center">
















</div>
📌 Sobre o Projeto

O Sistema de Acionamento Automatizado de Cancela utiliza Reconhecimento de Placas Veiculares (LPR) através de OpenCV + EasyOCR, integra-se a um backend FastAPI, um frontend Flask e controla fisicamente uma cancela por meio de Arduino (PySerial).

O objetivo é automatizar o fluxo de entrada/saída de veículos em pátios de locadoras, aumentando a eficiência e reduzindo erros operacionais.

📚 Sumário

🚀 Tecnologias Utilizadas

📦 Arquitetura do Sistema

🧩 Requisitos do Sistema

⚙️ Instalação e Configuração

▶️ Execução

🖥️ Como Usar

📸 Diagramas e Imagens

📄 Licença

🚀 Tecnologias Utilizadas
🧠 Visão Computacional

OpenCV

EasyOCR

🖥️ Backend

FastAPI

Python 3.9+

🌐 Frontend

Flask (substitui Streamlit)

HTML/CSS

🗄️ Banco de Dados

SQLite

SQLAlchemy

⚡ Hardware

Arduino (Uno/Nano)

Servo Motor

Webcam

PySerial

📦 Arquitetura do Sistema
flowchart LR
    CAM[📷 Webcam] --> LPR[🧠 OCR + OpenCV]
    LPR --> API[⚡ FastAPI]
    API --> DB[(🗄️ SQLite)]
    API --> FLASK[🌐 Flask]
    API --> ARD[🔌 Arduino - PySerial]
    ARD --> CANC[🚧 Cancela]

🧩 Requisitos do Sistema
Software

Python 3.9+

pip

Git

Arduino IDE

DB Browser for SQLite (opcional)

Hardware

Arduino (Uno/Nano)

Servo Motor

Webcam

⚙️ Instalação e Configuração
1️⃣ Preparar Arquivos
cd C:\Projetos\TCC

2️⃣ Criar Ambiente Virtual
python -m venv .venv
.\.venv\Scripts\activate   # Windows
source .venv/bin/activate  # Linux/macOS
pip install -r requirements.txt

3️⃣ Configurar Arduino

Abra a Arduino IDE

Conecte a placa

Carregue: arduino/cancela_control.ino

Escolha porta e placa

Envie o código

Anote a porta (ex.: COM3 ou /dev/ttyUSB0)

4️⃣ Criar Banco de Dados
python database/init_db.py


Cria: database/cancela.db

5️⃣ Configurar Porta Serial

No arquivo arduino/arduino_controller.py, edite:

serial.Serial('COM3', 9600)  # Windows
serial.Serial('/dev/ttyUSB0', 9600)  # Linux/macOS

▶️ Execução

A aplicação possui três serviços.
Todos devem estar com o ambiente virtual ativo.

Terminal 1 – API FastAPI
cd sistema_cancela/api
uvicorn main:app --host 0.0.0.0 --port 8000 --reload

Terminal 2 – Frontend Flask
cd sistema_cancela/app
python web_interface.py

Terminal 3 – Aplicação Principal
cd sistema_cancela/app
python main_app.py --arduino-port /dev/cu.usbmodem1201 --camera 0 --confidence 0.7

🖥️ Como Usar

Posicione a placa diante da webcam

O sistema irá:

Capturar a imagem

Processar com OpenCV + EasyOCR

Consultar banco de dados

Enviar comando ao Arduino

Abrir/fechar a cancela

Acesse painel web:

http://localhost:8080


Gerencie placas:

➕ Adicionar

✏️ Editar

📴 Inativar

📸 Diagramas e Imagens
📁 Estrutura do Projeto
sistema_cancela/
 ├── api/               # Backend FastAPI
 ├── app/               # Flask + Aplicação Principal
 ├── arduino/           # Código Arduino + controlador serial
 ├── database/          # SQLite + scripts
 ├── docs/images        # Diagramas e imagens
 └── requirements.txt