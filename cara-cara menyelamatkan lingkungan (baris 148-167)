# test-bot(bot class)
# This example requires the 'members' and 'message_content' privileged intents to function.

import discord
import random
import os
from discord.ext import commands
from bot_logic import gen_pass
import requests
lingkungan = {"kurangi penggunaan plastik": "dengan mengurangi penggunaan plastik, kita dapat mengurangi limbah plastik yang sulit terurai di lingkungan. gunakan tas belanja kain, hindari sedotan plastik, dan beli produk dengan kemasan minimal.",
    "daur ulang sampah": "pisahkan sampah organik dan anorganik, lalu daur ulang bahan seperti kertas, kaca, plastik, dan logam agar dapat digunakan kembali.",
    "bersihkan area sekitar": "adakan kegiatan membersihkan area sekitar rumah, taman, atau jalan bersama keluarga atau komunitas untuk menjaga kebersihan lingkungan.",
    "tanam pohon": "menanam pohon membantu menyerap karbon dioksida, memberikan oksigen, dan meningkatkan kualitas udara di sekitar.",
    "gunakan transportasi ramah lingkungan": "kurangi emisi dengan menggunakan transportasi umum, sepeda, atau berjalan kaki saat bepergian.",}

description = '''An example bot to showcase the discord.ext.commands extension
module.

There are a number of utility commands being showcased here.'''

intents = discord.Intents.default()
intents.members = True
intents.message_content = True
# command prefix 
bot = commands.Bot(command_prefix='$', description=description, intents=intents)


@bot.event
async def on_ready():
    print(f'Logged in as {bot.user} (ID: {bot.user.id})') # type: ignore
    print('------')

# adding two numbers
@bot.command()
async def add(ctx, left: int, right: int):
    """Adds two numbers together."""
    await ctx.send(left + right)

@bot.command()
async def subtract(ctx, left: int, right: int):
    """Subtracts two numbers together."""
    await ctx.send(left - right)

@bot.command()
async def multiply(ctx, left: int, right: int):
    """Multiplies two numbers together."""
    await ctx.send(left * right)

@bot.command()
async def divide(ctx, left: int, right: int):
    """Divides two numbers together."""
    await ctx.send(left / right)            

# spamming word
@bot.command()
async def repeat(ctx, times: int, content='repeating...'):
    """Repeats a message multiple times."""
    for i in range(times):
        await ctx.send(content)
        
# password generator        
@bot.command()
async def pw(ctx):
    await ctx.send(f'Kata sandi yang dihasilkan: {gen_pass(10)}')

# coinflip
@bot.command()
async def coinflip(ctx):
    num = random.randint(1,2)
    if num == 1:
        await ctx.send('It is Head!')
    if num == 2:
        await ctx.send('It is Tail!')

# rolling dice
@bot.command()
async def dice(ctx):
    nums = random.randint(1,6)
    if nums == 1:
        await ctx.send('It is 1!')
    elif nums == 2:
        await ctx.send('It is 2!')
    elif nums == 3:
        await ctx.send('It is 3!')
    elif nums == 4:
        await ctx.send('It is 4!')
    elif nums == 5:
        await ctx.send('It is 5!')
    elif nums == 6:
        await ctx.send('It is 6!')

        
# random local meme image
@bot.command()
async def meme(ctx):
    # menampilkan secara random
    img_name = random.choice(os.listdir('meme'))
    with open(f'meme/{img_name}', 'rb') as f:
    # with open(f'meme/enemies-meme.jpg', 'rb') as f:
        # Mari simpan file perpustakaan/library Discord yang dikonversi dalam variabel ini!
        picture = discord.File(f)
    await ctx.send(file=picture)

# overwriting kalimat.txt
@bot.command()
async def tulis(ctx, *, my_string: str):
    with open('kalimat.txt', 'w', encoding='utf-8') as t:
        text = ""
        text += my_string
        t.write(text)
# append kalimat.txt
@bot.command()
async def tambahkan(ctx, *, my_string: str):
    with open('kalimat.txt', 'a', encoding='utf-8') as t:
        text = "\n"
        text += my_string
        t.write(text)
# reading kalimat.txt
@bot.command()
async def baca(ctx):
    with open('kalimat.txt', 'r', encoding='utf-8') as t:
        document = t.read()
        await ctx.send(document)

# API to get random dog and duck image 
def get_dog_image_url():
    url = 'https://random.dog/woof.json'
    res = requests.get(url)
    data = res.json()
    return data['url']
@bot.command('dog')
async def dog(ctx):
    '''Setiap kali permintaan dog (anjing) dipanggil, program memanggil fungsi get_dog_image_url'''
    image_url = get_dog_image_url()
    await ctx.send(image_url)
def get_duck_image_url():
    url = 'https://random-d.uk/api/random'
    res = requests.get(url)
    data = res.json()
    return data['url']
@bot.command('duck')
async def duck(ctx):
    '''Setiap kali permintaan duck (bebek) dipanggil, program memanggil fungsi get_duck_image_url'''
    image_url = get_duck_image_url()
    await ctx.send(image_url)


@bot.command()
async def selamatkan(ctx):
    lingkungan = [
        "Berikut adalah beberapa cara untuk mengurangi sampah di lingkungan sekitar:",
        "1. kurangi penggunaan plastik",
        "2. daur ulang sampah",
        "3. bersihkan area sekitar",
        "4. tanam pohon",
        "5. gunakan transportasi ramah lingkungan",
        "Mohon untuk menulis analisis dengan prefixnya dan dilanjutkan dengan pilihan dari cara-cara tersebut TANPA nomornya DAN tanpa huruf kapital agar mendapatkan deskripsi lebih jelas cara tersebut bekerja.", 
    ]
    output = "\n".join(lingkungan)
    await ctx.send(output)

@bot.command() 
async def analisis(ctx, *, kalimat: str):
    if kalimat in lingkungan:
        await ctx.send(lingkungan[kalimat])
    else:
        await ctx.send("Kalimat tidak ditemukan.")
