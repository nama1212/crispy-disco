import requests
from cryptography.fernet import Fernet

# Generate a key for encryption
key = Fernet.generate_key()
cipher_suite = Fernet(key)

# Function to encrypt bookmarks
def encrypt_bookmark(bookmark):
    encrypted_bookmark = cipher_suite.encrypt(bookmark.encode())
    return encrypted_bookmark

# Function to decrypt bookmarks
def decrypt_bookmark(encrypted_bookmark):
    decrypted_bookmark = cipher_suite.decrypt(encrypted_bookmark).decode()
    return decrypted_bookmark

# Function to search DuckDuckGo
def search_duckduckgo(query):
    url = f"https://api.duckduckgo.com/?q={query}&format=json"
    response = requests.get(url)
    return response.json()

# Example usage
bookmark = "https://www.example.com"
encrypted = encrypt_bookmark(bookmark)
print(f"Encrypted Bookmark: {encrypted}")

# Decrypting the bookmark
decrypted = decrypt_bookmark(encrypted)
print(f"Decrypted Bookmark: {decrypted}")

# Searching DuckDuckGo
search_query = "Python programming"
search_results = search_duckduckgo(search_query)
print(f"Search Results for '{search_query}':")
print(search_results)
