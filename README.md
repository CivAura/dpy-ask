# 오류날 시 질문 방법
* 질문하기 위해 질문하지 말고 그냥 질문하세요.
  - 안좋은 예시) **오류가 나는데 이거 도와주실수 있으신분 있나요?** : `❌`
  - **코드와 함께 오류를 보여주세요.** 이때 주의할점은 전체 코드와(토큰같이 민감한 부분은 가리고 질문해주셔도 상관없어요) 오류를 주셔야합니다.
  - 또한 디스코드의 [ToS](https://discord.com/terms)를 위반하는 질문(복구봇, 자판기) 등등의 질문은 삼가해주세요.

# 자주 실수하는 오류들
1. 인텐트 문제
   * 인텐트 문제는 인텐트를 선언해주시지 않으셔서 생기는 오류입니다.
   * 해결 방법은 다음과 같습니다.
```py
# 파이썬의 기본 내장 함수가 아닌 다른 함수 혹은 다른 기능이 필요할 때 사용함
import discord, asyncio

client = discord.Client()

@client.event
async def on_ready(): # 봇이 실행되면 한 번 실행됨
    print("이 문장은 Python의 내장 함수를 출력하는 터미널에서 실행됩니다\n지금 보이는 것 처럼 말이죠")
    await client.change_presence(status=discord.Status.online, activity=discord.Game("봇의 상태매세지"))

@client.event
async def on_message(message):
    if message.content == "테스트": # 메세지 감지
        await message.channel.send ("{} | {}, Hello".format(message.author, message.author.mention))
        await message.author.send ("{} | {}, User, Hello".format(message.author, message.author.mention))


# 봇을 실행시키기 위한 토큰을 작성해주는 곳
client.run('토큰을 입력하세요')
```
   * adfasd
