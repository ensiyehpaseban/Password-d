import string


def encrypted(plain_text, k):
    alphabets = string.ascii_lowercase
    encrypted_text = ''
    for char in plain_text:
        if char in alphabets:
            new_char = alphabets[(alphabets.index(char) + k) % 26]
            encrypted_text += new_char
        else:
            encrypted_text += char
    return encrypted_text


def decrypted(cipher_text, k):
    alphabets = string.ascii_lowercase
    plain_text = ''
    for char in cipher_text:
        if char in alphabets:
            new_char = alphabets[(alphabets.index(char) - k) % 26]
            plain_text += new_char
        else:
            plain_text += char
    return plain_text


def brute_force_attack(cipher_text):
    possible_answers = []
    alphabets = string.ascii_lowercase
    for k in range(26):
        plain_text = ''
        for char in cipher_text:
            if char in alphabets:
                new_char = alphabets[(alphabets.index(char) - k) % 26]
                plain_text += new_char
            else:
                plain_text += char
        possible_answers.append(plain_text)
    return possible_answers


if name == "main":
    k = int(input("Enter the key for encryption (0-25): "))
    plain_text = input("Enter the text to encrypt: ")

    encrypted_text = encrypted(plain_text, k)
    print(f"Encrypted Text: {encrypted_text}")

    decrypted_text = decrypted(encrypted_text, k)
    print(f"Decrypted Text: {decrypted_text}")

    print("Brute-force Attack Results:")
    possible_answers = brute_force_attack(encrypted_text)
    for answer in possible_answers:
        print(answer)
