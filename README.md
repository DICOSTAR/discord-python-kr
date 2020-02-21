    async def on_message(self: object, message: object) -> object:
        if message.author == self.user:
            return
****c# 앞에 c를 삭제해주세요. 깃허브는 async부터 소스로 인식하지만 c#이 시작되는데 부터가 전부 소스입니다.
****엔터라고 써놓은 부분은 엔터눌러서 줄갈라주세요. 엔터 치고 (엔터) 지우기*****


c# 유저를 태그하여 밴시키고 뮤트시키는 방식보다 유저id가 훨씬 낫습니다. 유저가 서버를 나갔더라도 id를 입력해 차단가능합니다.
c# 문의 : 뗈쁉#2651


import discord(엔터)
 c# ↑pip install 필요 모듈 (cmd에 pip install discord 검색)(엔터)
import datetime(엔터)
import asyncio(엔터)
import random(엔터)
import time(엔터)

class MyClient(discord.Client):(엔터)
    async def on_ready(self):(엔터)
        assert isinstance(self.user, object)(엔터)
        print('봇이 성공적으로 부팅되었습니다.', self.user)(엔터)
        game = discord.Game("활동상태에 표시할 게임이름을 써주세요")(엔터)
        await client.change_presence(status=discord.Status.online, activity=game)(엔터)

    async def on_message(self: object, message: object) -> object:
        if message.author == self.user:
            return

        #욕설 변수값 **수동으로 추가하세요**
        dyrtjf = ["시발", "병신", "장애인", "섹스", "보지", "자지", "느금마", "니애미", "니애비", "후장", "느금빠", "ㅅㅂ"]

        # "디스코드주소"에 답하여 디스코드주소를 출력합니다.
        if message.content == '디스코드주소':
            await message.channel.send('디스코드주소를 입력해주세요')

        # "관리자"에 답하여 관리자 리스트를 출력합니다.
        if message.content == '관리자':
            await message.channel.send('관리자를 입력해주세요')

        # Custom Message
        if message.content == 'blank':
            await message.channel.send('blank')

        # !채널세시지 (CHANNEL.ID) (할말)을 입력하여 해당 채널에 메시지를 출력합니다.
        if message.content.startswith("!채널메시지"):
            channel = message.content[7:25]
            msg = message.content[26:]
            await client.get_channel(int(channel)).send(msg)
            await message.channel.send('해당 채널에 메시지를 보냈습니다.')

        # !dm (USER.ID) (할말)을 입력하여 해당 유저에게 메시지를 출력합니다.
        if message.content.startswith("!dm"):
            author = message.guild.get_member(int(message.content[4:22]))
            msg = message.content[23:]
            await author.send(msg)
            await message.channel.send('해당 유저에게 dm을 보냈습니다.')

        # !뮤트 (USER.ID) 로 해당 유저를 뮤트시킵니다. ▶역할 설정 필수◀
        if message.content.startswith("!뮤트"):
            author = message.guild.get_member(int(message.content[4:22]))
            role = discord.utils.get(message.guild.roles, name="※역할이름을 입력하세요※메시지보내기 설정 필수")
            await author.add_roles(role)
            await message.channel.send(f"유저 id {author.id}: 해당 유저를 뮤트시켰습니다.")
            print ('뮤트된 유저가 발생하였습니다.')

        # !전체삭제 로 최근 메세지 99개를 삭제합니다.
        if message.content.startswith("!전체삭제"):
            await message.channel.purge(limit=100)
            await message.channel.send('메세지 100개 삭제됨.')
            await message.channel.purge(limit=1)

        # !내정보 로 자신의 정보를 표시합니다.
        if message.content.startswith("!내정보"):
            date = datetime.datetime.utcfromtimestamp(((int(message.author.id) >> 22) + 1420070400000) / 1000)
            embed = discord.Embed(color=0xff00ff)
            embed.add_field(name="닉네임", value=message.author.name, inline=True)
            embed.add_field(name="서버 닉네임", value=message.author.display_name, inline=True)
            embed.add_field(name="디스코드가입일", value=str(date.year) + "/" + str(date.month) + "/" + str(date.day), inline=True)
            embed.add_field(name="디스코드주소: discord.gg/디스코드주소입력", value=message.author.name + "님 반가워요!", inline=True)
            embed.set_thumbnail(url=message.author.avatar_url)
            await message.channel.send(embed=embed)

        #욕설감지
        for word in dyrtjf:
            if message.content.count(word) > 0:
                print("욕설이 감지되어 삭제처리 되었습니다.")
                await message.channel.purge(limit=1)

        #욕설감지 메세지 출력
        for word in dyrtjf:
            author = message.guild.get_member(int(message.author.id))
            if message.content.count(word) > 0:
                await message.channel.send(f"{author.mention}욕설이 감지되어 삭제되었습니다. 지속적인 욕설 사용시 추방됩니다.")

        # !밴 (USER.ID) 로 해당 유저를 밴시킵니다. ▶밴 역할 설정 필수◀ 빼래배래뺀
        if message.content.startswith("!밴"):
            author = message.guild.get_member(int(message.content[3:21]))
            role = discord.utils.get(message.guild.roles, name="밴 역할이름을 적어주세요")
            await author.add_roles(role)
            await message.channel.send(f"유저 id {author.id}: 해당 유저를 밴시켰습니다.")
            print('밴된 유저가 발생하였습니다.')


client = MyClient()(엔터)
client.run('봇토큰을 입력하세요.)
