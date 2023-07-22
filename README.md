# 오류날 시 질문 방법
* 질문하기 위해 질문하지 말고 그냥 질문하세요.
  - 안좋은 예시) **오류가 나는데 이거 도와주실수 있으신분 있나요?** : `❌`
  - **코드와 함께 오류를 보여주세요.** 이때 주의할점은 전체 코드와(토큰같이 민감한 부분은 가리고 질문해주셔도 상관없어요) 오류를 주셔야합니다.
  - 또한 디스코드의 [ToS](https://discord.com/terms)를 위반하는 질문(복구봇, 자판기) 등등의 질문은 삼가해주세요.

# 자주 실수하는 오류들
1. 인텐트 문제
   [이런 오류](https://media.discordapp.net/attachments/877424201810718730/1030265390443532339/Screenshot_20221014_084638.png)
   * 인텐트 문제는 인텐트를 선언해주시지 않으셔서 생기는 오류입니다.
   * 해결 방법은 다음과 같습니다.
    1. `https://discord.com/developers/applications/봇id/bot`에 들어가서
     ㄴ여기중에 사용해야하는 권한을 켜줄수있습니다
    2.
    이제 python에서 권한을 켜야합니다
    INTENTS = discord.Intents.default()
    INTENTS.허용할 권한 = True # 없으면 안써도됩니다
    client = discord.Client(intents = INTENTS)

     ㄴ이런식으로 하나씩 권한을 하거나 모든 권한을 추가하고싶다면
    INTENTS = discord.Intents.all()
    client = discord.Client(intents = INTENTS)

     ㄴ아니면 이런식으로 모든 권한을 다킬수 있습니다

    주의사항
    * 아래문구를 보기전에: 만약 위코드를 안쓰고 실행했는데 오류가 안뜬다면 pip install discord --upgrade를 써서 dpy버저을 업그레이드 해야합니다
    1. 만약 메세지로 작동하는 봇을 만들려한다면
    INTENTS = discord.Intents.default()
    INTENTS.messages = True # 메세지를 읽는권한
    INTENTS.message_content = True # 메세지를 읽는권한
    client = discord.Client(intents = INTENTS)

    ㄴ 이렇게 메세지를 읽는권한을 켜주셔야합니다
    2. 만약 discord dev사이트(https://discord.com/developers/applications)에서 intent를 안키고 python코드에서만 키셨다면 오류가 발생할겁니다

    https://discordpy.readthedocs.io/en/stable/intents.html
     ㄴ자세한건 여기에서 확인하세요

