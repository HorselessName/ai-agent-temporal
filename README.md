# ==========================================
# Setup do projeto (Windows PowerShell + uv)
# Python 3.10 fixo pro projeto
# ==========================================

# 0) LIMPEZA (se você realmente quer "do zero" no mesmo diretório)
#    (CUIDADO: isso apaga config e venv do projeto)
Remove-Item -Recurse -Force .venv -ErrorAction SilentlyContinue
Remove-Item -Force uv.lock, pyproject.toml, .python-version -ErrorAction SilentlyContinue

# 1) (Opcional) Descobrir onde está seu Python 3.10 (launcher do Windows)
py -0p

# 2) Inicializar o projeto já mirando no Python 3.10
uv init -p 3.10 .

# 3) Garantir o PIN do Python do projeto (isso fixa a versão no .python-version)
uv python pin 3.10

# 4) (Opcional, mas recomendado) Travar o range no pyproject.toml
#    Abra o pyproject.toml e deixe assim:
#    requires-python = ">=3.10,<3.11"

# 5) Criar / sincronizar o ambiente do projeto (vai criar a .venv)
uv sync

# 6) Adicionar dependências (vai atualizar pyproject.toml + uv.lock + .venv)
uv add python-dotenv fastapi jinja2 litellm stripe temporalio uvicorn requests

# 7) Validar que tá rodando em 3.10 dentro do ambiente do projeto
uv run python -V

# 8) Se você quiser ativar o venv no terminal (opcional)
.\.venv\Scripts\Activate.ps1
python -V
