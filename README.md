# chocobi 초코비 조의 프로젝트를 소개합니다
# 목차
  - [😋팀 소개](#-팀-소개)
  - [📂프로젝트 소개](#-프로젝트-소개)
  - [🫶개발과정](#-개발과정)
  - [📑기능 명세서](#-기능-명세서)
  - [🖥️code](#-code)
  - [✨ppt link](#-ppt-link)
# 팀 소개
안녕하세요 저희는 코린이들이 모인
초코비 팀입니다!
저희는 처음 팀을 결성할 때
'초'보 '코'딩 '비'기너로서
많은 것을 배우고 가자라는 의미로
팀명을 결정했습니다.
그렇다면 저희 팀은 어떤 구성원으로 이루어져 있을까요?

♠️ 오정
# 프로젝트 소개
# 개발 과정
# 기능 명세서
# code
-# tkinter를 사용하기 위한 import
  from tkinter import *
  from tkinter import ttk
  import pandas as pd

-# 아이디, 패스워드 초기 배열 생성
  ID = ['chocobi', 'frozen']
  PW = ['imgroot', 'anna']

-# tkinter 객체 생성
  window = Tk()

-# 사용자 id와 password를 저장하는 변수 생성
  user_id, password = StringVar(), StringVar()
  sign_id, sign_pw = StringVar(), StringVar()


-# 사용자 id와 password를 비교하는 함수
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


-# 사용자가 입력한 id와 pw를 list에 추가하는 함수
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
              ttk.Label(window_error, text='''# Is your ID or PW 8~20 letters # entered ID is already in ID list''').grid(row=1, column=1, padx=10, pady=10)
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


-# id와 password, 그리고 확인 버튼의 UI를 만드는 부분
  ttk.Label(window, text="Identification : ").grid(row=0, column=0, padx=10, pady=10)
  ttk.Label(window, text="Password : ").grid(row=1, column=0, padx=10, pady=10)
  ttk.Entry(window, textvariable=user_id).grid(row=0, column=1, padx=10, pady=10)
  ttk.Entry(window, textvariable=password, show='*').grid(row=1, column=1, padx=10, pady=10)
  ttk.Button(window, text="Login", command=check_data).grid(row=2, column=1, padx=10, pady=10)
  ttk.Button(window, text="Move to Sign up page", command=append_data).grid(row=2, column=0, padx=10, pady=10)

  window.mainloop()

# ppt link
