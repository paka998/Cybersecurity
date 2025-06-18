🔒 **Title:**
Secure Text Hiding in Images Using Steganography and XOR Encryption

🧩 **Problem Statement:**
Steganography is the art of hiding information within other seemingly harmless data.
In this project, we aim to securely embed a secret text into an image file in such a way that the existence of the hidden message is imperceptible to the human eye. 
This technique ensures an additional layer of security where communication does not raise suspicion. 
Traditional encryption methods make data unreadable, but steganography hides the fact that communication is even taking place. 
The objective is to encrypt the text using XOR operation and modify specific pixels in an image accordingly, and then to decrypt it back successfully.

**System Approach**

**1.System Requirements:**

Python 3.8+, Jupyter/Colab, OpenCV, NumPy, Matplotlib

**2.Libraries Required:**

cv2 (OpenCV) – for image processing

numpy – for numerical operations

matplotlib.pyplot – to visualize images

os, string – for basic file and character operations

**Algorithm & Deployment (Step-by-Step)**

Load the image using OpenCV

Convert image to RGB and display

Read and store ASCII values of the message and key

Encrypt: XOR each character's ASCII value with the corresponding key character

Modify image pixels accordingly

Save the encrypted image

Decrypt: Reverse the XOR process using the same key

Retrieve the original hidden message


🔐 **Steganography Using XOR in Image Pixels**

import cv2

import numpy as np

import os

import matplotlib.pyplot as plt

import String

# ASCII mapping dictionaries
d = {chr(i): i for i in range(255)}

c = {i: chr(i) for i in range(255)}

# Load the image
image_path = "your_image.png"  # Change to your image path

x = cv2.imread(image_path)

x_rgb = cv2.cvtColor(x, cv2.COLOR_BGR2RGB)

plt.imshow(x_rgb)

plt.axis('off')

plt.title("Original Image")

plt.show()

print("Image shape (Height, Width, Channels):", x.shape)

# Input key and text to hide
key = "216416624"

text = "seetha"

# Convert to ASCII values
text_ascii = [d[ch] for ch in text]

key_ascii = [d[ch] for ch in key]

# Encrypt and modify pixel values
x_enc = x.copy()

n = m = z = kl = 0

l = len(text)

for i in range(l):

    orig_val = x_enc[n, m, z]
    
    new_val = text_ascii[i] ^ key_ascii[kl]
    
    x_enc[n, m, z] = new_val
    
    print(f"Embedding '{text[i]}' (ASCII {text_ascii[i]}) XOR '{key[kl]}' (ASCII {key_ascii[kl]}) = {new_val} at pixel({n},{m},{z})")
    
    n += 1
    
    m += 1
    
    m = (m + 1) % 3
    
    z = (z + 1) % 3
    
    kl = (kl + 1) % len(key)

# Save the encrypted image
cv2.imwrite("encrypted_image.png", x_enc)

print("Encrypted image saved as 'encrypted_image.png'")

# Display encrypted image
plt.imshow(cv2.cvtColor(x_enc, cv2.COLOR_BGR2RGB))

plt.axis('off')

plt.title("Encrypted Image")

plt.show()

# Decryption process
decrypt = ""

n = m = z = kl = 0

for i in range(l):

    val = x_enc[n, m, z]
    
    orig_char = c[val ^ key_ascii[kl]]
    
    decrypt += orig_char
    
    print(f"Decrypting pixel({n},{m},{z}): {val} XOR {key_ascii[kl]} = {val ^ key_ascii[kl]} -> '{orig_char}'")
    
    n += 1
    
    m += 1
    
    m = (m + 1) % 3
    
    z = (z + 1) % 3
    
    kl = (kl + 1) % len(key)

print("Decrypted text:", decrypt)

**Conclusion**

This project successfully demonstrates a basic image steganography technique using XOR-based encryption. 

The hidden text was embedded into specific image pixels and was later retrieved with 100% accuracy.

The method ensures visual integrity of the image while maintaining data secrecy. 

Some challenges include maintaining pixel integrity and scaling for larger messages. 

Future improvements could involve more complex encoding schemes and use of multiple image formats.

