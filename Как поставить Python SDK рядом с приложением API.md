

# FISCO BCOS Python SDK
Python SDK предоставляет Python API для FISCO BCOS. Использование FISCO BCOS Python SDK позволяет легко и быстро разрабатывать блокчейн-приложения на основе FISCO-BCOS.
https://github.com/FISCO-BCOS/python-sdk

Требования: 
- Среда Python: Python 3.6+, включая 3.9.x, 3.10.
- Узел FISCO BCOS: https://fisco-bcos-doc.readthedocs.io/zh-cn/latest/docs/quick_start/air_installation.html
- Зависимости UBUNTU:
    ```commandline
    sudo apt install -y zlib1g-dev libffi6 libffi-dev wget git
    ```

# Как поставить Python SDK рядом с приложением app
- Переименовать python-sdk в python_sdk, т.к. python не любит в импортах модули через тире.
- Создать папку python_sdk/bin/solc, скачать нужную версию solidity в эту папку https://github.com/FISCO-BCOS/solidity/releases, разархивировать. 
- Скопировать client_config.py.template в client_config.py
- Исправить в client_config.py:
  ```contract_dir = "python_sdk/contracts"
  - contract_info_file = "python_sdk/bin/contract.ini" 
  - account_keyfile_path = "python_sdk/bin/accounts" 
  - solc_path = "python_sdk/bin/solc/solc"
  - solcjs_path = "python_sdk/solcjs"
  - gm_solc_path = "python_sdk/bin/solc/solc-gm"
  - bcos3_lib_path = "python_sdk/bcos3sdklib"
  - bcos3_config_file = "python_sdk/bcos3sdklib/bcos3_sdk_config.ini"
  ```
  - Заменить все адреса 127.0.0.1 на адрес сервера с развернутым узлом. Если ставите рядом с узлом, то нужно смотреть внутрений адрес, на котором развернут узел. Например для FISCO-BCOS Pro это 172.25.0.3
- Скопировать bcos3sdklib/bcos3_sdk_config_sample.ini в bcos3sdklib/bcos3_sdk_config.ini
- Выполните скрипт python download_c_lib.py. Если не работает, то в скрипте в строке ```filedownloader.download_file_with_progress(url,fname,proxies=net_proxy)```
нужно поставить ```proxies = None```
- В файле bcos3_sdk_config.ini:
  - установить значение ```ca_path=python_sdk/bin```
  - заменить 127.0.0.1 на адрес, который писали в client_config.py
  - добавить рядом с node.0 еще одну ноду: node.1={Адрес}:20201
- Скопировать из папки с узлом в папку python_sdk/bin следующие сертификаты и ключи. Например в развернутом узле Pro они лежат по адресу BcosBuilder/pro/generated/rpc/chain0/agencyBBcosRpcService/172.25.0.3/sdk
:
  ```
  - ca.crt
  - cert.cnf
  - sdk.crt
  - sdk.key
  - sdk.nodeid
  ```
  
- В папку contracts засунуть abi файлы контрактов TFactory и EqToken
- В папку bin/accounts кинуть pem файлы аккаунтов, под которым надо будет дергать апи

В pyproject.toml приложения API уже записаны зависимости python-sdk, поэтому устанавливать их из requirements.txt не надо

    
# Консоль Python SDK
Если нужно использовать консоль, то нужно:
1) создать виртуальное окружение в папке python_sdk и активировать его
2) установить зависимости python_sdk
   ```pip install -r requirements.txt```
3) подняться на одну папку вверх и вызвать консоль python_sdk
   ```python3 python_sdk/console3.py usage```
    

    