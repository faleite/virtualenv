# Ambientes virtuais e instalação de bibliotecas

#### PIP - Pip Install Package.
**É uma maneira de instalar pacotes externos (3-party) no nosso ambiente.**

Comando|Função
-------|------
**pip isntall pylint**| *Instalar a biblioteca pylint*
**pip show pylint**| *Mostra informações sobre a biblioteca e quais bibliotecas ela depende*
*Listar bibliotecas instaladas frizando sua versões*| **pip freeze**
*Desinstalar biblioteca*| **pip uninstall pandas**
*Listar bibliotecas instaladas*| **pip list**
*Atualizar pip ou outra biblioteca*| **pip install --upgrade pip**

Exemplo:
```sh
$ pip show pylint
Name: pylint
Version: 2.14.4
Summary: python code static checker
Home-page:
Author: Python Code Quality Authority
Author-email: code-quality@python.org
License: GPL-2.0-or-later
Location: /Users/fabricio/.pyenv/versions/3.10.5/lib/python3.10/site-packages
Requires: astroid, dill, isort, mccabe, platformdirs, tomli, tomlkit
Required-by:
```
---

#### VENV - Ambiente Virtual
**Uma ferramenta para "hackear" o site-packages.**
- Cria um ambiente "local"
- Isolado do "Global"
- Vem embutido no Python

Função|Comando
------|-------
*Criar um ambiente Virtual*| **python -m venv <nome_do_ambiente>**
*Ativar o ambiente Virtual (Unix)*| **source <venv>/bin/activate**
*Desativar o ambiente virtual*| **deactivate**


Fragmentos da Função|Comando
---|---
*Pedir para o python executar um módulo*| **-m**
*Módulo Virtual Env*| **venv**

*venv é uma biblioteca do python (venv é uma biblioteca parcial do virtualenv)
virtualenv é biblioteca completa e externa ao python (para instalar: $ pip install virtualenv)*

---

#### requirements.txt - Arquivos de dependêcias do projeto

*Exemplo de arquivo requirements.txt*
```sh
# requirements.txt

# pacotes que quero instalar
httpx
pandas
pytest

# pacotes com versões específicas
black == 0.6.1 # igual a 0.6.1
django >= 4.1.1 # maior que 4.1.1
flask != 3.5 # diferente de 3.5
selenium ~= 1.1 # maior ou igual a 1.1, mas menor que 2
```
*Documentaçao do [requirements.txt](hhttps://pip.pypa.io/en/stable/reference/requirements-file-format/)*

Para instalar as bibliotecas seguindo a padronização do requirements:
```sh
$ pip install -r requirements.txt
```

*Bibliotecas externas do python [pypi](https://pypi.org)*
*Recomendações de bibliotecas:* **pip-autoremove, pipdeptree**

Função|Comando
------|-------
*Remove a biblioteca e suas bibliotecas dependentes| **pip-autoremove pandas**
*Lista o que cada biblioteca instalou*| **pip install pipdeptree**

**Nem todas as bibliotecas vão para o ambiente de produção, para isso utilizamos outros arquivos de
requirements para separar os ambientes.**

*Exemplo* **Ambiente de Dev com o requirements_dev.txt**
```sh
# requirements_dev.txt

-r requirements.txt # instala as bibliotecas de produção

# Instala as bibliotecas de desenvolvimento
ipdb # debugger
ipython # shell interativo
black # formatador de código
```

---

#### constraints.txt "Arquivo de restrições"

- *As vezes, por alguma limitação, decidimos que algumas bibliotecas TEM que estar em
versões específicas. Por homologação, seguração, limitação do sistema e etc...*
- *Para esses casos, existe o arquivo constraints.txt*
- *Tem o mesmo formato do requirements.txt, mas não instala as bibliotecas, só força versões específicas*

Função|Comando
------|-------
*Uso no ambiente de desenvolvimento*| pip install -r requirements_dev.txt -c constraints.txt
*Uso no ambiente de produção*| pip install -r requirements.txt -c constraints.txt

#### Outras ferramentas

*Amigos do pip:*
- **pip-autoremove**: Remove do ambiente as bibliotecas dependentes
- **pipdeptree**: Mostra quais bibliotecas depende de quais

*Amigos do venv:*
- **virtualenvwrapper**: Facilita a criação e manutenção dos ambientes

*Amigos do Python:*
- **pyenv**: Instala várias versões de python no ambiente
- **tox**: Roda testes em versões diferentes do python
- **pipx**: Instala ferramentas de linha de comando em um ambiente
virtual isolado, **bom para instalações globais**

*Para o ambiente cientifico*

No ambiente de programação cientifica vamos nos deparar com outras ferramentas:
- Conda: Gerenciador de pacotes como o pip
- miniconda: Distribuição Python + Conda
- Anaconda: Distribuição do Python com muitos pacotes científicos
- Mamba: Parecido com o miniconda, mas refaz o conda em C++ para
performance

*Dica de gerênciamento de ambiente mais atual:*
- Pyenv: Várias versões do python
- pipx: Instalação de ferramentas globais
    - blue
    - httpie
    - poetry
    - ipython
- Poetry:
    - Gerenciador de ambiente virtual (venv)
    - Gerenciador de empacotamento (setup.py + setup.cfg)
    - Metadados do pacote (setup.py)
    - Instalação de bibliotecas (pip)
    - Gerenciador de versões de bibliotecas (requirements.txt)

*Saiba mais:*
>live [#179](https://www.youtube.com/watch?v=ZOSWdktsKf0) Gerênciando pacotes e ambientes com Poetry \
>live [#192](https://www.youtube.com/watch?v=O3bs4JtHrow) Como organizar um projeto python? \
>live [#162](https://www.youtube.com/watch?v=cEkA9PH2oEk) Sua aplicação NÃO está segura

*Estamos em fase de transição do empacotamento / gerenciamento de ambientes.
O requirements.txt + requirements_dev.txt + setup.py serão subsistidos pelo **pyproject.toml***
