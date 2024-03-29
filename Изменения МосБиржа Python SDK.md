
# FISCO BCOS Python SDK
Python SDK предоставляет Python API для FISCO BCOS. Использование FISCO BCOS Python SDK позволяет легко и быстро разрабатывать блокчейн-приложения на основе FISCO-BCOS.
https://github.com/FISCO-BCOS/python-sdk

По сравнение с версией FISCO BCOS в версии МосБиржи были некоторые изменения, для удобства работы и ускорения разработки. В Данном документе будут описываться все изменения, которые были внесены в этот проект.

- В файле python_sdk/bcos3sdk/bcos3client.py:
    - В методе init_clib_sdk:
        строка ```self.bcossdk = NativeBcos3sdk()``` изменена на
        ```python
        self.bcossdk = NativeBcos3sdk(self.config.bcos3_config_file, self.config.bcos3_lib_path)
        ```
    - В методе __init__ добавлен current_account
        ```python
         def __init__(self, current_account: str = None, client_config_instance=client_config):
                self.current_account = current_account
        ```
    - В методе load_default_account изменено определение аккаунта при ECDSA
      ```python
      if self.config.crypto_type == CRYPTO_TYPE_ECDSA:
              acc = self.current_account if self.current_account else self.config.account_keyfile
              self.account_file = "{}/{}".format(self.config.account_keyfile_path,
                                                 acc)
      ```
- В файле datatype_parser.py 
  - в методе parse_output используется get_fn_abi_types вместо get_fn_abi_types_single, а также decode_abi вместо decode_single




- Обновлены файлы utils/abi.py, utils/events.py и eth_utils/abi.py. Первые два в соответствии с этими изменениями: https://github.com/ethereum/web3.py/pull/2211/files#diff-c684b214ca53fc68c712e18a429fe7e01879dcfdefa14232a6417a60abd642e0.
А третий из этого коммита: https://github.com/ethereum/eth-utils/commit/d609ffb255427a74b976855d2d81aebfa3a967ab#diff-9dd3a111de9d7c55600844aa4e9f243028dae713650573ae72d11b9fea5bdb26
