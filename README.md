from PIL import Image

def encrypt_image(image_path, key):
    img = Image.open(image_path)
    width, height = img.size
    pixels = img.load()
    
    for y in range(height):
        for x in range(width):
            r, g, b = pixels[x, y]
            r = (r + key) % 256
            g = (g + key) % 256
            b = (b + key) % 256
            pixels[x, y] = (r, g, b)
    
    encrypted_image_path = image_path.replace('.png', '_encrypted.png')
    img.save(encrypted_image_path)
    print("Image encrypted successfully!")

def decrypt_image(encrypted_image_path, key):
    img = Image.open(encrypted_image_path)
    width, height = img.size
    pixels = img.load()
    
    for y in range(height):
        for x in range(width):
            r, g, b = pixels[x, y]
            r = (r - key) % 256
            g = (g - key) % 256
            b = (b - key) % 256
            pixels[x, y] = (r, g, b)
    
    decrypted_image_path = encrypted_image_path.replace('_encrypted.png', '_decrypted.png')
    img.save(decrypted_image_path)
    print("Image decrypted successfully!")

# Example usage:
image_path = "example.png"
key = 10  # You can change the key to any integer
encrypt_image(image_path, key)
decrypt_image("example_encrypted.png", key)
