import os
import requests

# Get the Etherscan API key from the environment variable
api_key = os.getenv("ETHERSCAN_API_KEY")
if not api_key:
    raise Exception("API key not found. Please set the ETHERSCAN_API_KEY environment variable.")

def get_eth_balance(address, api_key):
    url = "https://api.etherscan.io/api"
    params = {
        "module": "account",
        "action": "balance",
        "address": address,
        "tag": "latest",
        "apikey": api_key
    }
    response = requests.get(url, params=params)
    data = response.json()

    if data["status"] == "1":
        balance = int(data["result"]) / (10 ** 18)  # Convert from Wei to Ether
        return balance
    else:
        raise Exception("Error fetching balance: " + data["message"])

# Example usage:
address = "0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae"
try:
    balance = get_eth_balance(address, api_key)
    print(f"Balance for address {address}: {balance} ETH")
except Exception as e:
    print(e)export ETHERSCAN_API_KEY="FEHBE23A62CIWBPZCK6KM3FT7K8TPTRRPA"# Import
