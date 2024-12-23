import discord
import os
from dotenv import load_dotenv
from discord.ext import commands
load_dotenv()

intents = discord.Intents.all()
TOKEN = os.getenv("bot_token")

bot = commands.Bot(command_prefix='!', intents=intents)

if TOKEN is None:
    print("Bot token is not set")
else:

    @bot.event
    async def on_ready():
        print(f'Logged in as {bot.user}')

    @bot.event
    async def on_message(message):
        if message.author == bot.user:
            return

        if message.content.startswith('!hello'):
            await message.channel.send('Hello!')

        await bot.process_commands(message)

    @bot.command()
    async def purge(ctx,amount):
        if(amount.isdigit()):
            amount=int(amount)
            if(amount<1):
                await ctx.send("Amount must be Greater than 0")
                return

            deleted=await ctx.channel.purge(limit=amount+1)
            await ctx.send(f"{len(deleted)-1} Message ki gand maar di",delete_after=1.5)
            await ctx.send(f"Purged {len(deleted)-1} Messages",delete_after=30)
        else:
            await ctx.send("Africa ke lun, Number dal chup chap",delete_after=1.5)
            await ctx.message.delete()

    @bot.command()
    async def clsuser(ctx,user: discord.Member):
        delete=0
        async for message in ctx.channel.history(limit=500):  
            if delete >= 100:
                break
            if message.author==user:
                await message.delete()
                delete += 1

        await ctx.send(f"Purged {delete} from {user.display_name}",delete_after=30)
        await ctx.message.delete()


    @bot.command()
    async def clsbots(ctx):
        delete = 0
        async for message in ctx.channel.history(limit=500):  
            if delete >= 100:
                break
            if message.author.bot:
                await message.delete()
                delete += 1

        await ctx.send(f"Purged {delete} Bot Messages",delete_after=30)
        await ctx.message.delete()

    @bot.command()
    async def cls(ctx):
        delete = 0
        async for message in ctx.channel.history(limit=400):  
            if delete >= 100:
                break
            if not(message.author.bot):
                await message.delete()
                delete += 1

        await ctx.send(f"Purged {delete} Messages of Users",delete_after=30)

bot.run(TOKEN)
