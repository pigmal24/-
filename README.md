# chocobi 초코비 조의 프로젝트를 소개합니다
# 목차
  - [😋팀 소개](#-팀-소개)
  - [📂프로젝트 소개](#-프로젝트-소개)
  - [🫶Ground Rule](#-Ground-Rule)
  - [📑기능 명세서](#-기능-명세서)
  - [🖥️code](#-code)
  - [✨ppt link}(#-ppt-link)
# 팀 소개
안녕하세요 저희는 코린이들이 모인
초코비 팀입니다!
저희는 처음 팀을 결성할 때
'초'보 '코'딩 '비'기너로서
많은 것을 배우고 가자라는 의미로
팀명을 결정했습니다.
그렇다면 저희 팀은 어떤 구성원으로 이루어져 있을까요?

♠️ 오지은\(아 이거 뭐지\)

\#팀장 \#CSV 파일을 활용하여 병원의 종류 구분 \#그 위치를 지도에 표시

♣️ 김윤진

\#팀원 \#CSV 파일을 활용하여 병원 주소 추출 \#지도에 병원 위치 표시

♥️ 최연우

\#팀원 \#로그인 시스템 개발 \#회원가입 시스템 개발

♦️ 황진욱

\#팀원 \#CSV 파일 조사를 통한 서비스 구축 기반 마련 \#PPT 제작

# 프로젝트 소개

의료접근성 프로젝트:병원INFO 프로젝트는 

🏥의료기관의 위치🏥를 시각화하여 사용자에게 제공하는 것입니다. 

이를 지속 가능한 관점에서 바라보면, 

사용자들이 의료기관을 효율적으로 이용할 수 있도록

정보를 제공함으로써 

지역 사회의 건강한 삶을 지원하고, 

의료 리소스의 효율적인 활용을 촉진하는 역할을 합니다. 


"좀 더 자세하게 이야기를 하자면, "

지방 의료 서비스 접근성 저하로 발생하는 

의료 소멸 문제를 해결하기 위해 시작되었습니다. 

이 프로젝트는 Python을 활용하여 

지역 내 병원 정보를 수집하고 시각화하여 사용자에게 제공합니다. 

이를 통해 사용자들은 주변 의료 기관을 쉽게 찾을 수 있으며, 

의료 서비스에 대한 접근성이 향상됩니다.

또한, 이러한 프로젝트는 지속 가능한 의료 서비스 제공에 기여하고, 지역 사회의 건강한 발전을 촉진할 것으로 기대됩니다.

# Ground Rule
# 기능 명세서
# code
-# tkinter를 사용하기 위한 import
from tkinter import *
from tkinter import ttk
import pandas as pd

# 아이디, 패스워드 초기 배열 생성
ID = ['chocobi', 'frozen']
PW = ['imgroot', 'anna']

# tkinter 객체 생성
window = Tk()

# 사용자 id와 password를 저장하는 변수 생성
user_id, password = StringVar(), StringVar()
sign_id, sign_pw = StringVar(), StringVar()


# 사용자 id와 password를 비교하는 함수
def check_data():
    id = user_id.get()
    pw = password.get()
    inid = 0
    inpw = 0
    indexid, indexpw = 0, 0

    for i in ID:
        indexid += 1
        if id == i:
            inid = 1
            break

    for j in PW:
        indexpw += 1
        if pw == j:
            inpw = 1
            break

    if inid == 1 and inpw == 1 and indexid == indexpw:
        window_success = Tk()
        window_success.title("Success")
        ttk.Label(window_success, text="successfully logged in").grid(row=1, column=1, padx=10, pady=10)
        window_success.geometry("250x150+700+400")


        df = pd.read_csv("병원1.csv", engine='python')
        df = df[df['시도명'] == "대구광역시"].copy()
        df.loc[df['상권업종중분류명'].str.contains("병원"), "종류"] = '병원'
        df.loc[df['상권업종중분류명'].str.contains("약국/한약방"), "종류"] = '약국/한약방'
        import folium
        lat = df['위도'].mean()
        long = df['경도'].mean()
        m = folium.Map([lat, long], zoom_start=12)
        for i in df.index:
            sub_lat = df.loc[i, "위도"]
            sub_long = df.loc[i, '경도']

            title = f'{df.loc[i, "상호명"]}-{df.loc[i, "도로명주소"]}'
            if df.loc[i, '종류'] == '병원':
                color = "blue"
            elif df.loc[i, "종류"] == '약국/한약방':
                color = "red"
            folium.CircleMarker([sub_lat, sub_long],
                                radius=4,
                                color=color,
                                tooltip=title).add_to(m)
        m.show_in_browser()

    else:
        window_error = Tk()
        window_error.title("Error")
        ttk.Label(window_error, text="Check your Identification or Password").grid(row=1, column=1, padx=10, pady=10)
        window_error.geometry("250x150+700+400")


# 사용자가 입력한 id와 pw를 list에 추가하는 함수
def append_data():
    def sign_up():
        id = sign_id.get()
        pw = sign_pw.get()

        if 8 <= len(id) < 20 and 8 <= len(pw) < 20 and id not in ID:
            ID.append(id)
            PW.append(pw)
            window_success = Tk()
            window_success.title("Success")
            ttk.Label(window_success, text="successfully signed up").grid(row=1, column=1, padx=10, pady=10)
            window_success.geometry("250x150+700+400")

        else:
            window_error = Toplevel(window)
            window_error.title("Error")
            ttk.Label(window_error, text='''# Is your ID or PW 8~20 letters
# entered ID is already in ID list''').grid(row=1, column=1, padx=10, pady=10)
            window_error.geometry("250x150+700+400")

    window_signup = Toplevel(window)
    window_signup.title("Sign up")
    window_signup.geometry("300x200+700+400")

    # 회원가입 id와 password의 UI를 만드는 부분
    ttk.Label(window_signup, text="New ID : ").grid(row=0, column=0, padx=10, pady=10)
    ttk.Label(window_signup, text="New Password : ").grid(row=1, column=0, padx=10, pady=10)
    ttk.Entry(window_signup, textvariable=sign_id).grid(row=0, column=1, padx=10, pady=10)
    ttk.Entry(window_signup, textvariable=sign_pw).grid(row=1, column=1, padx=10, pady=10)
    ttk.Button(window_signup, text="Sign up", command=sign_up).grid(row=2, column=1, padx=10, pady=10)


# id와 password, 그리고 확인 버튼의 UI를 만드는 부분
ttk.Label(window, text="Identification : ").grid(row=0, column=0, padx=10, pady=10)
ttk.Label(window, text="Password : ").grid(row=1, column=0, padx=10, pady=10)
ttk.Entry(window, textvariable=user_id).grid(row=0, column=1, padx=10, pady=10)
ttk.Entry(window, textvariable=password, show='*').grid(row=1, column=1, padx=10, pady=10)
ttk.Button(window, text="Login", command=check_data).grid(row=2, column=1, padx=10, pady=10)
ttk.Button(window, text="Move to Sign up page", command=append_data).grid(row=2, column=0, padx=10, pady=10)

window.mainloop()

# ppt link
