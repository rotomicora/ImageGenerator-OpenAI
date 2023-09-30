
# ImageGenerator-OpenAI

**Un sencillo generador de imágenes mediante la API de [OpenAI](https://openai.com)**

# Ejemplos

> **Estos son algunos ejemplos**


<img src="https://user-images.githubusercontent.com/48841069/212538282-561de162-adf5-41af-8b23-d49b7a8c4894.png" alt="Perro con ojos verdes, un aura purpura y bultos en la cabeza" height="200px"> <img src="https://user-images.githubusercontent.com/48841069/212538452-27a92c3c-4742-43ff-8112-56dc67920b5f.png" alt="Niño con animacion realista jugando al fútbol" height="200px"> <img src="https://user-images.githubusercontent.com/48841069/212538746-12bb5f24-2b92-47bc-af71-3b10e2986d4a.png" alt="Sustancia roja en en un recipiente con grumos" height="200px">

# Codigo

```python
import os # Importamos la libreria OS, para poder usar comandos de consola
import random # Importamos la libreria random, para poder generar un nombre de archivo aleatorio
import string # Importamos la libreria string, para poder asignar unos parametros a la variable del nombre de archivo
import openai # Importamos la libreria de open ai, la cual nos permite usar la api de open ai
import requests # Importamos la libreria requests, para poder descargar la imagen generada
from colorama import Fore # Y por ultimo importamos Fore desde la libreria de Colorama, para darle un poco de color a la consola

os.system("cls") # Limpiamos la consola

# Y aquí  definimos las variables de los colores para tenerlos mas ordenados
w = Fore.LIGHTWHITE_EX
r = Fore.LIGHTRED_EX
g = Fore.LIGHTGREEN_EX
b = Fore.LIGHTBLUE_EX
y = Fore.LIGHTYELLOW_EX
m = Fore.LIGHTMAGENTA_EX
c = Fore.LIGHTCYAN_EX
black = Fore.LIGHTBLACK_EX



openai.organization = "ORGANIZACION_ID_AQUI" # Aquí debes poner el ID de tu organizacion que puedes encontrar en -> https://beta.openai.com/account/org-settings
openai.api_key = "OPENAI-APIKEY-AQUI" # Aquí debes poner tu API KEY que puedes encontrar en -> https://beta.openai.com/account/api-keys
openai.Model.list() 

os.system("title franafp - Image Generator - OPEN AI") # Aquí le damos un titulo a la consola

print(f"{m}[{w}1{m}] {black}Generador de imágenes") 


def image_gen(): # Aquí definimos la funcion de la generacion de imagenes
    image=input(f"{m}[{w}>>>{m}] {black}Deja tus argumentos aquí?:{w} ") # Aquí pedimos los argumentos para la imagen
    print(f"{m}[{w}>{m}] {black}Generando imagen{m}...")
    r = openai.Image.create(prompt=image, n=2, size="1024x1024") # Aquí le decimos a la api que genere la imagen con los argumentos que le dimos
    image_url = r["data"][0]["url"] # Aquí le decimos que guarde la url de la imagen generada
    os.system("cls")
    print(f"{m}[{w}!{m}] {black}Imagen generada: {y}{image_url}")
    print(f"{image_url}")
    save=input(f"{m}[{w}>>>{m}] {black}Quieres guardar la imagen? [y/n]:{w} ") # Aquí le preguntamos si quiere guardar la imagen
    if save == "y": # Si la respuesta es "y" entonces...
        path="./img/" # Aquí le decimos que guarde la imagen en la carpeta "img"
        nombre_random= "".join(random.choice(string.ascii_letters + string.digits)  for i in range(10)) # Aquí le decimos que genere un nombre aleatorio para la imagen
        nombre_archivo = f"{path}{nombre_random}.png" # Aquí le decimos que guarde la imagen con el nombre aleatorio y la extension .png
        imagen_save= requests.get(image_url).content # Aquí le decimos que descargue la imagen"
        with open(nombre_archivo, 'wb') as i:
            i.write(imagen_save)
            print(f"{m}[{w}!{m}] {black}Imagen guardada en: {y}{nombre_archivo}")
    openask=input("¿Quieres abrir la imagen? [y/n]: ") # Aquí le preguntamos si quiere abrir la imagen en el explorador
    if openask == "y": # Si la respuesta es "y" entonces...
        os.system(f"""explorer {image_url}""") # Aquí le decimos que abra la imagen en el explorador
    else: # Y si la respuesta es cualquier otra, entonces simplemente le decimos que salga del programa pulsando cualquier tecla
        print("OK")
        print("Pulsa cualquier tecla para salir")
        os.system("pause >nul")
        os.system("exit")

image_gen()

```
