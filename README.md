# Bot-vs-la-contaminacion
import discord
import random,os
from bot_logic import gen_pass
from discord.ext import commands
import requests

intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='$', intents=intents)
La variable intents almacena los privilegios del bot
intents = discord.Intents.default()

intents.members = True

Activar el privilegio de lectura de mensajes
intents.message_content = True
Crear un bot en la variable cliente y transferirle los privilegios
client = discord.Client(intents=intents)



@bot.command()
async def mem(ctx):
    img_name=random.choice(os.listdir('images'))
    with open(f'images/{img_name}', 'rb') as f:
        # ¡Vamos a almacenar el archivo de la biblioteca Discord convertido en esta variable!
        picture = discord.File(f)
    # A continuación, podemos enviar este archivo como parámetro.
    await ctx.send(file=picture)




def get_duck_image_url():
    url = 'https://random-d.uk/api/random'
    res = requests.get(url)
    data = res.json()
    return data['url']

@bot.command('duck')
async def duck(ctx):
    '''Una vez que llamamos al comando duck, 
    el programa llama a la función get_duck_image_url'''
    image_url = get_duck_image_url()
    await ctx.send(image_url)

bot.run('')
