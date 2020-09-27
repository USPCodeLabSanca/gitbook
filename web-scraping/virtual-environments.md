# Virtual Environments

Uma **Virtual Enviroment** é um ambiente isolado que contém versão e pacotes instalados de um projeto em Python.

Seu objetivo é **evitar conflitos de dependencia** com a **versões e pacotes entre projetos**.

Usualmente, há uma virtual environment por projeto, que:

- **É "externa" ao código**: Não se codifica dentro da virtualenv, que é uma pasta no mesmo nível do projeto. 
- **Não deve ser incluída no fluxo de git**: Adiciona-se a pasta ao `.gitignore`.

Os **nomes dos pacotes utilizados devem ser salvos em um `requirements.txt`**. Usualmente, é o único **arquivo** necessário para **criar um ambiente baseado em uma lista de dependências** pré-definidas.

## Instalar Virtualenv

```bash
pip install virtualenv
```

## Criar virtualenv

### Alternativa 1: Apontando caminho completo para diretório do Python desejado. 
```bash
virtualenv --python='/usr/local/bin/python3' virtualenv_name
```

### Alternativa 2: Shortcut
```bash
virtualenv -p $(which python3) virtualenv_name
```
Cria um ambiente baseado no python3 global do sistema (Caso exista).

## Ativar virtualenv

```bash
source virtualenv_name/bin/activate
```

Após ativar a máquina virtual, seu nome deve aparecer entre parênteses antes de cada comando no terminal ```$ (virtualenv_name)```

## Instalar pacotes
Após entrar no ambiente, basta usar a sintaxe padrão:

```bash
pip install nome_do_pacote
```
## Instalar requirements.txt

```bash
pip install -r requirements.txt
```

## Salvar dependências instaladas em um requirements.txt

```bash
pip freeze --local > requirements.txt
```
O argumento --local força que apenas dependências locais (instaladas no virtualenv) sejam salvas. Retirá-lo faz que com dependencias globais também sejam salvas.

## Adicionando virtualenv ao .gitignore

```bash
echo "virtualenv_name/">> .gitignore
```
## Saindo da virtualenv

```bash
deactivate
```

Sai do ambiente e remove indicativo ```$ (virtualenv_name)``` do terminal.

## Recomendações de estudo sobre virtualenv
[Artigo de Vinícius Ramos - PythonAcademy](https://pythonacademy.com.br/blog/python-e-virtualenv-como-programar-em-ambientes-virtuais)

[Documentação](https://virtualenv.pypa.io/en/latest/index.html)