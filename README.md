home-sensores
Descrição
Aplicação Python que integra sensores Tuya Smart (fumo e vazamento de água) via Tuya Cloud, sensores locais (temperatura, humidade, COV, formaldeído, CO₂ e fumo) via TinyTuya, e apresenta uma interface web interativa com NiceGUI. Envia alertas em tempo real através de um servidor ntfy quando são detetadas condições críticas.

Funcionalidades
Leitura Cloud

Deteta estado de fumo e vazamento de água

Monitora percentagem de bateria dos sensores

Leitura Local

Mede temperatura, humidade, compostos orgânicos voláteis (COV), formaldeído e CO₂

Detecta fumo local

Interface Web (NiceGUI)

Exibe sessões ativas e timestamp da última atualização

Ícones de estado (verde/vermelho) e barras de progresso para bateria

Gráficos de linha históricos empilhados verticalmente

Atualização dinâmica:

Cloud: a cada 5 s se houver browser ativo, ou 30 s sem

Local: a cada 10 s com browser, ou 30 s sem

Alertas (ntfy)

Notificações em transição de estado (False→True) para fumo ou água

Alertas locais para temperatura, humidade, COV, CO₂ e fumo

Pré-requisitos
Python 3.10+

Dependências (instalar via pip):

bash
Copiar
Editar
pip install nicegui tinytuya tuya-connector requests
Configuração
No início do script (testes.py ou similar), defina:

python
Copiar
Editar
ACCESS_ID       = "seu_access_id"
ACCESS_SECRET   = "seu_access_secret"
REGION_URL      = "https://openapi.tuyaeu.com"
DEVICE_ID_FIRE  = "id_do_sensor_de_fumo_cloud"
DEVICE_ID_WATER = "id_do_sensor_de_agua_cloud"

# Sensor local ambiental (TinyTuya)
ENV_DEV_ID      = "id_do_sensor_ambiental"
ENV_LOCAL_KEY   = "local_key_ambiental"
ENV_IP          = "IP_do_sensor_ambiental"
ENV_VERSION     = 3.5

# Sensor local de fumo (TinyTuya)
SMOKE_DEV_ID    = "id_do_sensor_de_fumo_local"
SMOKE_LOCAL_KEY = "local_key_fumo"
SMOKE_IP        = "IP_do_sensor_de_fumo"
SMOKE_VERSION   = 3.5

# Servidor ntfy
NTFY_URL        = "http://<host>:<porta>/Alertas"
NTFY_USER       = "usuario_ntfy"
NTFY_PASS       = "senha_ntfy"
Execução
bash
Copiar
Editar
python testes.py
A interface ficará disponível em:

arduino
Copiar
Editar
http://localhost:8089
Estrutura do Código
read_cloud() (thread): conecta à Tuya Cloud e atualiza state_cloud

get_sensor_data() (async): lê sensores locais via TinyTuya

main_page(): define layout e elementos NiceGUI

update_ui() (timer): atualiza UI, gráficos e envia alertas

ui.run(port=8089): inicia o servidor web

Boas Práticas
Use Git para controlo de versões:

bash
Copiar
Editar
git init
echo "venv/\n__pycache__/" > .gitignore
git add .
git commit -m "📦 Inicializa projeto home-sensores"
Crie tags ou branches para marcos estáveis.
