# Pixel-Manipulation-For-Image-Encryption
PIX To Image Encrypt

from PIL import Image

def encrypt_image(image_path, output_path, shift):
    image = Image.open(image_path)
    pixels = image.load()

    for i in range(image.width):
        for j in range(image.height):
            r, g, b = pixels[i, j]
            # Add shift and keep values in valid RGB range 0-255
            r_encrypted = (r + shift) % 256
            g_encrypted = (g + shift) % 256
            b_encrypted = (b + shift) % 256
            pixels[i, j] = (r_encrypted, g_encrypted, b_encrypted)

    image.save(output_path)
    print(f"Image encrypted and saved as {output_path}")

def decrypt_image(image_path, output_path, shift):
    image = Image.open(image_path)
    pixels = image.load()

    for i in range(image.width):
        for j in range(image.height):
            r, g, b = pixels[i, j]
            # Subtract shift and keep values valid
            r_decrypted = (r - shift) % 256
            g_decrypted = (g - shift) % 256
            b_decrypted = (b - shift) % 256
            pixels[i, j] = (r_decrypted, g_decrypted, b_decrypted)

    image.save(output_path)
    print(f"Image decrypted and saved as {output_path}")

# User Input
image_file = input("Enter input image file path: ")
shift_value = int(input("Enter shift value (0-255): "))
action = input("Type 'encrypt' to encrypt or 'decrypt' to decrypt the image: ").lower()
output_file = input("Enter output image file path: ")

if action == "encrypt":
    encrypt_image(image_file, output_file, shift_value)
elif action == "decrypt":
    decrypt_image(image_file, output_file, shift_value)
else:
    print("Invalid action selected.")
    
