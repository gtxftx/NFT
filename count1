secrets = openai_secret_manager.get_secrets("opensea")
api_key = secrets["api_key"]

# Import the requests library to make HTTP requests
import requests

# Define the OpenSea API endpoint
endpoint = "https://api.opensea.io/api/v1/assets"

# Define the function to count the number of NFTs in a collection
def count_nfts_in_collection(contract_address, collection_name):
    # Make a GET request to the OpenSea API to retrieve the assets
    params = {
        "contract_address": contract_address,
        "metadata": f"collection:{collection_name}",
        "limit": 1000,
        "offset": 0,
    }
    headers = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {api_key}",
    }
    response = requests.get(endpoint, params=params, headers=headers)

    # Check the status code of the response
    if response.status_code == 200:
        # Extract the assets from the response
        assets = response.json()["assets"]
        # Return the number of assets
        return len(assets)
    else:
        # Raise an exception if the request failed
        raise ValueError(f"Failed to retrieve assets: {response.text}")

# Example usage
contract_address = "0x06012c8cf97BEaD5deAe237070F9587f8E7A266d"
collection_name = "My Cool Collection"
nft_count = count_nfts_in_collection(contract_address, collection_name)
print(f"Number of NFTs in collection '{collection_name}': {nft_count}")
