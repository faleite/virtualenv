# Ambientes virtuais e instalação de bibliotecas

#### VENV - Ambiente Virtual
**Uma ferramenta para "hackear" o site-packages.**
- Cria um ambiente "local"
- Isolado do "Global"
- Vem embutido no Python

Comando| Função
-------|-------
**python -m venv <nome_do_ambiente>**| *Criar um ambiente Virtual*
**source <venv>/bin/activate**| *Ativar o ambiente Virtual (Unix)*
**deactivate**| *Desativar o ambiente virtual*


Fragmentos da Função|Comando
---|---
*Pedir para o python executar um módulo*| **-m**
*Módulo Virtual Env*| **venv**

*venv é uma biblioteca do python (venv é uma biblioteca parcial do virtualenv)
virtualenv é biblioteca completa e externa ao python, para instalar:* ``$ pip install virtualenv``

---

#### PIP - Pip Install Package.
**É uma maneira de instalar pacotes externos (3-party) no nosso ambiente.**

Comando|Função
-------|------
**pip isntall pylint**| *Instalar a biblioteca pylint*
**pip show pylint**| *Mostra informações sobre a biblioteca e quais bibliotecas ela depende*
**pip freeze**| *Listar bibliotecas instaladas frizando sua versões*
**pip uninstall pandas**| *Desinstalar biblioteca*
**pip list**| *Listar bibliotecas instaladas*
**pip install --upgrade pip**| *Atualizar pip ou outra biblioteca*
**pip list -o**| *Listar bibliotecas mostrando se estão atualizadas*
**pip install --upgrade <pacote\>**| Atualizar biblioteca


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

#### requirements.txt - Arquivos de dependêcias do projeto

*Exemplo de arquivo requirements.txt*
```sh
# requirements.txt

# pacotes que quero instalar na ultima verção
httpx
pandas
pytest

# pacotes com versões específicas
flake8 > 1.0.0 # Versões maiores que 1.0.0
pylint < 2.0.0 # Versões menores que 2.0.0
fastapi <= 3.0.0 # Versões menores ou iguais a 3.0.0
black == 0.6.1 # igual a 0.6.1
django >= 4.1.1 # maiores ou iguais a 4.1.1
flask != 3.5 # diferente de 3.5
selenium ~= 1.0.1 # maior ou igual a 1.0.1, mas menor que 1.1.0
matlab ~= 1.1 # maior ou igual a 1.0, mas menor que 2.0
doctest == 1.1.* # maior verção do patch 1.1.0, 1.1.1, 1.1.2 -> pega a 1.1.2

# Alternativa com combinados
pacote >= 3.0, <4.0
pacote >= 3.0, <=4.0
```

*Pode criar o requirements.txt com pip freeze:*

``$ pip freeze > requirements.txt``

*Instalar as bibliotecas seguindo a padronização do requirements:*

``$ pip install -r requirements.txt``

*Documentaçao do [requirements.txt](hhttps://pip.pypa.io/en/stable/reference/requirements-file-format/)*\
*Bibliotecas externas do python [pypi](https://pypi.org)*

*Recomendações de bibliotecas:* **pip-autoremove e pipdeptree**

Função|Comando
------|-------
**pip-autoremove pandas**| *Remove a biblioteca e suas bibliotecas dependentes*
**pip install pipdeptree**| *Lista o que cada biblioteca instalou*


**Nem todas as bibliotecas vão para o ambiente de produção.**\
**Para isso utilizamos outros arquivos de requirements para separar os ambientes.**

#### Ambiente de Dev com o requirements_dev.txt

*Exemplo:*

```sh
# requirements_dev.txt

-r requirements.txt # instala as bibliotecas de produção

# Instala as bibliotecas de desenvolvimento
ipdb # debugger
ipython # shell interativo
black # formatador de código
```

#### constraints.txt "Arquivo de restrições"

- *As vezes, por alguma limitação, decidimos que algumas bibliotecas TEM que estar em
versões específicas. Por homologação, seguração, limitação do sistema e etc...*
- *Para esses casos, existe o arquivo constraints.txt*
- *Tem o mesmo formato do requirements.txt, mas não instala as bibliotecas, só força versões específicas*

Função|Comando
------|-------
*Uso no ambiente de desenvolvimento*| pip install -r requirements_dev.txt -c constraints.txt
*Uso no ambiente de produção*| pip install -r requirements.txt -c constraints.txt

---
#### Ferramentas para controle de atualizações dependêcias
---

*Existem frentes diferentes e regras diferentes em cada projeto/empresa:*

- pre-commit: Cria um script no git (pasta hook) que informa atualizações antes de commitar
- Integração contínua
- pip-upgrader: pacote  a ser instalado com o pip
- [pyup](https://www.pyup.io): segurança de dependências

---
#### Safety - Ferramenta para validação de vulnerabilidades
---

Comando|Função
-------|------
**pip install safety**| *Instala o pacote para checar vulnerabilidades*
**safety check**| *Verifica e lista as vulnerabilidades dos pacotes instalados*
**safety check -r requirements.txt --full-report**|

*Este processo pode ser automatizado com:*

- pre-commit
- Integração contínua
- dependa-bot (github)
- pipenv check


---
#### Outras ferramentas
___

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
>live [#163](https://www.youtube.com/watch?v=cEkA9PH2oEk) Sua aplicação NÃO está segura

*Estamos em fase de transição do empacotamento / gerenciamento de ambientes.
O requirements.txt + requirements_dev.txt + setup.py serão subsistidos pelo **pyproject.toml***
