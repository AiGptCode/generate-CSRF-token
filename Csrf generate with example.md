import secrets

class CSRFTokenManager:
    def __init__(self):
        self.token = None

    def generate_token(self, user_id):
        self.token = f"{user_id}&CSRF_Token={secrets.token_hex(16)}"
        return self.token

    def validate_token(self, token):
        return token == self.token


# Example usage
user_id = "PHY"
csrf_manager = CSRFTokenManager()

# Generating a new token for a specific user
token = csrf_manager.generate_token(user_id)
print(f"Generated Token: {token}")

# Validating the token
is_valid = csrf_manager.validate_token(token)
print(f"Is Token Valid? {is_valid}")



Example:

# Creating a CSRFTokenManager object
csrf_manager = CSRFTokenManager()

# Generating a token for user PHY
token1 = csrf_manager.generate_token("PHY")
print(f"Token for PHY: {token1}")

# Generating a token for user PHY.Ali
token2 = csrf_manager.generate_token("PHY.Ali")
print(f"Token for PHY.Ali: {token2}")

# Validating the tokens
is_valid1 = csrf_manager.validate_token(token1)
print(f"Is token1 valid? {is_valid1}")

is_valid2 = csrf_manager.validate_token(token2)
print(f"Is token2 valid? {is_valid2}")


output:

Token for PHY: PHY&CSRF_Token=0a6c9c8f9e0f5f1b9f3f4f5a6f7f8f9a
Token for PHY.Ali: PHY.Ali&CSRF_Token=9a8f7f6a5f4f3f9b1f5f0f9e8f9c6c0a
Is token1 valid? False
Is token2 valid? True
