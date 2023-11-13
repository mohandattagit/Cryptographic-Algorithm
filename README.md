# Cryptographic-Algorithm
Chien's Group Authentication Scheme involves complex cryptographic operations
##CODE....................................................................................................................
import hashlib
import random

# Chien's Group Authentication Scheme
class ChiensGroupAuthentication:
    def __init__(self, group_members):
        self.group_members = group_members
        self.group_keys = {}

    def generate_keys(self):
        for member in self.group_members:
            private_key = random.randint(1, 1000)
            public_key = hashlib.sha256(str(private_key).encode()).hexdigest()
            self.group_keys[member] = {
                'private_key': private_key,
                'public_key': public_key
            }

    def authenticate_group(self, received_keys):
        for member, key_data in received_keys.items():
            if member in self.group_members:
                if key_data['public_key'] != hashlib.sha256(str(self.group_keys[member]['private_key']).encode()).hexdigest():
                    return False
            else:
                return False
        return True

# Example Usage
if __name__ == "__main__":
    members = ['Device1', 'Device2', 'Device3']
    chiens_auth = ChiensGroupAuthentication(members)

    # Generate keys for each group member
    chiens_auth.generate_keys()

    # Simulate sending and receiving keys
    received_keys = {}
    for member in members:
        received_keys[member] = {
            'public_key': chiens_auth.group_keys[member]['public_key']
        }

    # Authenticate the group
    authentication_result = chiens_auth.authenticate_group(received_keys)

    if authentication_result:
        print("Group authentication successful.")
    else:
        print("Group authentication failed.")

