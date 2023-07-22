# 오류날 시 질문 방법
* 질문하기 위해 질문하지 말고 그냥 질문하세요.
  - 안좋은 예시) **오류가 나는데 이거 도와주실수 있으신분 있나요?** `❌`
  - **코드와 함께 오류를 보여주세요.** 이때 주의할점은 전체 코드와(토큰같이 민감한 부분은 가리고 질문해주셔도 상관없어요) 오류를 주셔야합니다.
  - 또한 디스코드의 [ToS](https://discord.com/terms)를 위반하는 질문(복구봇, 자판기) 등등의 질문은 삼가해주세요.

# 자주 실수하는 오류들
## 1. 인텐트 문제
  * 위와 같은 오류는 인텐트 문제는 **인텐트를 선언해주시지 않으셔서** 생기는 오류입니다.
  * 해결 방법은 다음과 같습니다. `👇`
  ### 1. 웹사이트에서 켜기
  * [디스코드 디벨로퍼 포탈](https://discord.com/developers/applications)에 들어가셔서,
  * 자신의 봇에 들어가셔서 왼쪽의 `Bot`탭을 눌러서 아래로 내리면 **Privileged Gateway Intents**가 있는데, 그곳에서
  ```
  PRESENCE INTENT
  SERVER MEMBERS INTENT
  MESSAGE CONTENT INTENT
  ```
  * `👆️` 위의 권한 3개를 모두 켜주셔야 합니다.
  ### 2. 코드에서 켜기
  ```py
  INTENTS = discord.Intents.default()
  INTENTS.권한 = True
  client = discord.Client(intents = INTENTS)
  ```
  * 이런식으로 하나씩 권한을 추가해도 됩니다.
  ```py
  INTENTS = discord.Intents.all()
  client = discord.Client(intents = INTENTS)
  ```
  * 저는 위에 과정을 더 선호하는 편입니다.
  - 웹사이트와 코드에서 **모두** 켜야하며,
  - 더 자세한 오류 해결 방법은 [여기](https://discordpy.readthedocs.io/en/stable/intents.html)에서 확인해주세요.
## 2. **모듈 미설치 오류**
  * 모듈 미설치 오류는 말 그대로 `discord`모듈을 설치하지 않으셔서 발생하는 오류입니다.
  * `ModuleNotFoundError: No Module named 'discord'`이런 식으로 오류 메세지가 나며 타 모듈도 해결 방법이 똑같습니다.
  * 오류 해결 방법은 간단합니다. 터미널에 들어가셔서 `pip install discord`를 치면 해결이 되는 문제로, 만약 쳤을때 다음과 같은 오류가 난다면,
  ```
  'pip'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다.
  ```
  * 이럴때는 환경 변수 문제입니다. 환경 변수 설정은 [여기](https://anys4udoc.readthedocs.io/en/latest/attach/zz-python-install.html)를 참고해주세요.
## 기타 오류 & 자주 물어보는 것
### 1. DiscordComponents문제
  * DiscordComponents라는 모듈은 이제 더이상 사용하지 못하는 모듈입니다. 모종의 이유로 pypi에서 사라졌기 때문입니다.
  * 대신 [discord.py](https://discordpy.readthedocs.io/en/stable) `2.0`버전에서 사용할 수 있습니다. 그리고 또한 비슷한 모듈을 [PyPI](https://pypi.org)에서 찾아볼 수 있습니다.
### 2. 여러가지 기능을 넣고싶어요!
  * 파이썬은 오버로딩을 지원하지 않습니다. 실행관련코드로 예시를 들어드리겠습니다.
  - 다음은 잘못된 예시입니다.
  ```py
  import discord, asyncio

  INTENTS = discord.Intents.all() 
  client = discord.Client(intents = INTENTS)

  @client.event
  async def on_ready():
      print("이 문장은 Python의 내장 함수를 출력하는 터미널에서 실행됩니다\n지금 보이는 것 처럼 말이죠")
      await client.change_presence(status=discord.Status.online, activity=discord.Game("봇의 상태매세지"))

  @client.event
  async def on_message(message):
      if message.content == "테스트":
          await message.channel.send("첫번째 명령어")

  @client.event
  async def on_message(message):
      if message.content == "안녕":
          await message.channel.send("두번째 명령어")

  client.run('토큰을 입력하세요')
  ```
  - 파이썬은 오버로딩을 지원하지 않기 때문에 `@client.event`, `async def..`까지는 다시 쓰지 않으셔도 됩니다. 다음은 잘 된 예시입니다.
  ```py
  import discord, asyncio

  INTENTS = discord.Intents.all() 
  client = discord.Client(intents = INTENTS)

  @client.event
  async def on_ready():
      print("이 문장은 Python의 내장 함수를 출력하는 터미널에서 실행됩니다\n지금 보이는 것 처럼 말이죠")
      await client.change_presence(status=discord.Status.online, activity=discord.Game("봇의 상태매세지"))

  @client.event
  async def on_message(message):
      if message.content == "테스트":
          await message.channel.send("첫번째 명령어")

      if message.content == "안녕":
          await message.channel.send("두번째 명령어")

  client.run('토큰을 입력하세요')
  ```
  * 이런식으로 작성해야 잘 작동합니다.
### 구글링 하는 방법
  * 구글링을 하는 방법은 간단합니다. 다음은 오류가 나서 어떻게 고칠지 구글링을 하는 잘 된 예시입니다.
    - `python discord.py intents` [사용하는 언어 + 사용하는 모듈 + 기능 아니면 오류코드]으로 검색하시면 됩니다.
  * 참고로 파이썬의 기본 기능같이 한국어로 된 도움말이 많은 경우는 한국어로 질문하셔도 상관없습니다.
  * 그리고 문장으로 검색하시면 검색 결과가 잘 안나옵니다. 다음은 문장으로 검색했을때의 안좋은 예시입니다.
    - `how to fix intents error python discord.py`
  * 다음은 별로 좋지 못한 구글링 방법입니다. 초보들이 가장 많이하는 실수중 하나입니다.
    - `파이썬으로 디스코드봇 만들기 오류` [한국어 + 문장]한국사람중에 파이썬으로 discord.py모듈을 사용하여 디스코드 봇을 만드는 사람이 잘 없을것 같죠? 이러면 검색결과가 잘 안나옵니다.
# 마지막으로 마치며..
* 이 문서가 처음 디스코드 봇을 만드려는 뉴비들에게 많은 도움이 되셨으면 좋겠습니다. 감사합니다.
* 그리고 질문하기 전에 구글링은 필수입니다! 진짜 열심히 만들었습니다.
