# chocobi 초코비 조의 프로젝트를 소개합니다
# 목차
  - [😋팀 소개](#-팀-소개)
  - [📂프로젝트 소개](#-프로젝트-소개)
  - [🫶개발과정](#-개발과정)
  - [🖥️code](#-code)

# 팀 소개
안녕하세요 저희는 코린이들이 모인
초코비 팀입니다!
저희는 처음 팀을 결성할 때
'초'보 '코'딩 '비'기너로서
많은 것을 배우고 가자라는 의미로
팀명을 결정했습니다.
그렇다면 저희 팀은 어떤 구성원으로 이루어져 있을까요?

♠️ 오지은(웹크롤링, 지도 시각화 개발)
팀장, 컴퓨터학부 플랫폼소프트웨어
♠️ 김윤진(웹크롤링, 지도 시각화 개발)
팀원, 컴퓨터학부 플랫폼소프트웨어
♠️ 최연우(로그인/회원가입 개발)
팀원, 컴퓨터학부 글로벌소프트웨어
♠️ 황진욱(CSV 기반파일 조사, PPT 제작)
팀원, 식물의학과

# 프로젝트 소개
의료접근성 프로젝트:병원INFO 프로젝트는 
지방 의료 서비스 접근성 저하로 발생하는 의료 소멸 문제를 해결하기 위해 시작되었습니다. 
이 프로젝트는 Python을 활용하여 지역 내 병원 정보를 수집하고 시각화하여 사용자에게 제공합니다. 
이를 통해 사용자들은 주변 의료 기관을 쉽게 찾을 수 있으며, 의료 서비스에 대한 접근성이 향상됩니다.
또한, 이러한 프로젝트는 지속 가능한 의료 서비스 제공에 기여하고, 지역 사회의 건강한 발전을 촉진할 것으로 기대됩니다.

본 프로젝트의 목적은 의료기관의 위치를 시각화하여 사용자에게 제공하는 것입니다. 
이를 지속 가능한 관점에서 바라보면, 사용자들이 의료기관을 효율적으로 이용할 수 있도록
정보를 제공함으로써 지역 사회의 건강한 삶을 지원하고, 의료 리소스의 효율적인 활용을 촉진하는 역할을 합니다. 

# 개발 과정

1) 로그인/회원가입
Tkinter를 사용하여 간단한 로그인 및 회원가입 시스템을 구현하였습니다.

Tkinter 라이브러리 import 및 객체 생성: 코드의 첫 부분에서는 Tkinter 라이브러리를 import하고, Tk() 메서드를 사용하여 window 객체를 생성합니다. 이 객체는 프로그램의 메인 창 역할을 합니다.

사용자 데이터 초기화: 코드의 두 번째 부분에서는 사용자의 초기 데이터(ID 및 PW)를 배열로 설정합니다. 이 배열은 로그인 및 회원가입 시 데이터를 검증하는 데 사용됩니다.

로그인 및 회원가입 기능 구현: check_data() 함수는 사용자가 입력한 ID와 PW를 검증하여 로그인 성공 또는 실패에 따라 메시지 창을 표시합니다. append_data() 함수는 새로운 사용자가 회원가입하는 기능을 구현합니다.

회원가입 창 생성: append_data() 함수 내부에서 sign_up() 함수를 호출하여 새로운 회원가입 창을 생성합니다. 사용자는 이 창에서 새로운 ID와 PW를 입력하고, 입력이 유효한 경우 회원가입이 완료됩니다.

UI 구성: ttk.Label, ttk.Entry, ttk.Button을 사용하여 사용자 인터페이스를 구성합니다. 각각은 텍스트 라벨, 입력 필드, 버튼을 생성하는 Tkinter 위젯입니다.

메인 루프 실행: window.mainloop()를 호출하여 Tkinter 이벤트 루프를 실행합니다. 이는 사용자의 입력을 받고, 프로그램이 종료될 때까지 GUI를 업데이트합니다.

이러한 과정을 통해 코드는 간단한 로그인 및 회원가입 시스템을 구현하고, Tkinter를 사용하여 사용자 인터페이스를 만들어냅니다.

2) 지도 시각화 과정

CSV 데이터파일 필터링을 통해 pandas를 사용하여 CSV 파일을 읽고, 해당 지역의 데이터만 필터링합니다.

Folium 지도 생성을 통해 folium 라이브러리를 사용하여 평균 위도와 경도를 중심으로 하는 지도를 생성합니다.

지도에서 시각화 정보를 제공합니다. 데이터 프레임을 순회하면서 각 병원과 약국/한약방의 위치에 CircleMarker를 추가하고, 색상을 구분하여 지도에 표시합 후 생성된 지도를 기본 웹 브라우저에서 열어줍니다.

# code
  #tkinter를 사용하기 위한 import
  from tkinter import *
  from tkinter import ttk
  import pandas as pd
  from folium.plugins import MiniMap
  import folium

  #아이디, 패스워드 초기 배열 생성
  ID = ['chocobi', 'frozen']
  PW = ['imgroot', 'anna']

  #tkinter 객체 생성
  window = Tk()

  #사용자 id와 password를 저장하는 변수 생성
  user_id, password = StringVar(), StringVar()
  sign_id, sign_pw = StringVar(), StringVar()

  #사용자 id와 password를 비교하는 함수
  def check_data():
      id = user_id.get()
      pw = password.get()
      inid = 0
      inpw = 0
      indexid, indexpw = 0, 0
  
      for i in ID :
          indexid += 1
          if id == i:
              inid = 1
              break
      
      for j in PW :
          indexpw += 1
          if pw == j:
              inpw = 1
              break
      
      if inid == 1 and inpw == 1 and indexid == indexpw:
          window_success = Tk()
          window_success.title("Success")
          ttk.Label(window_success, text = "successfully logged in").grid(row = 1, column = 1, padx = 10, pady = 10)
          window_success.geometry("250x150+700+400")
  
          df=pd.read_csv("병원.csv",engine='python')
          df=df[df['시도명']=="대구광역시"].copy()
          df.loc[df['상권업종중분류명'].str.contains("병원"),"종류"]='병원'
          df.loc[df['상권업종중분류명'].str.contains("약국/한약방"),"종류"]='약국/한약방'
          
          lat=df['위도'].mean()
          long=df['경도'].mean()
          m=folium.Map([lat,long],zoom_start=12)
          for i in df.index:
              sub_lat=df.loc[i,"위도"]
              sub_long=df.loc[i,'경도']
  
              title=f'{df.loc[i,"상호명"]}-{df.loc[i,"도로명주소"]}'
              if df.loc[i,'종류']=='병원':
                  color="blue"
              elif df.loc[i,"종류"]=='약국/한약방':
                  color="red"
              folium.CircleMarker([sub_lat,sub_long],
                                  radius=5,
                                  color=color,
                                  popup=title).add_to(m)
          
          minimap = MiniMap()
          m.add_child(minimap) 
          m.show_in_browser()
  
      else:
          window_error = Tk()
          window_error.title("Error")
          ttk.Label(window_error, text = "Check your Identification or Password").grid(row = 1, column = 1, padx = 10, pady = 10)
          window_error.geometry("250x150+700+400")
        
  #사용자가 입력한 id와 pw를 list에 추가하는 함수
  def append_data():
      def sign_up() :
          id = sign_id.get()
          pw = sign_pw.get()
      
          if 8 <= len(id) < 20 and 8 <= len(pw) < 20 and id not in ID :
              ID.append(id)
              PW.append(pw)
              window_success = Tk()
              window_success.title("Success")
              ttk.Label(window_success, text = "successfully signed up").grid(row = 1, column = 1, padx = 10, pady = 10)
              window_success.geometry("250x150+700+400")
  
          else:
              window_error = Toplevel(window)
              window_error.title("Error")
              ttk.Label(window_error, text = '''# Is your ID or PW 8~20 letters # entered ID is already in ID list''').grid(row = 1, column = 1, padx = 10, pady = 10)
              window_error.geometry("250x150+700+400")
  
      window_signup = Toplevel(window)
      window_signup.title("Sign up")
      window_signup.geometry("300x200+700+400")

      #회원가입 id와 password의 UI를 만드는 부분
      ttk.Label(window_signup, text = "New ID : ").grid(row = 0, column = 0, padx = 10, pady = 10)
      ttk.Label(window_signup, text = "New Password : ").grid(row = 1, column = 0, padx = 10, pady = 10)
      ttk.Entry(window_signup, textvariable = sign_id).grid(row = 0, column = 1, padx = 10, pady = 10)
      ttk.Entry(window_signup, textvariable = sign_pw).grid(row = 1, column = 1, padx = 10, pady = 10)
      ttk.Button(window_signup, text = "Sign up", command = sign_up).grid(row = 2, column = 1, padx = 10, pady = 10)

    
    
  #id와 password, 그리고 확인 버튼의 UI를 만드는 부분
  ttk.Label(window, text = "Identification : ").grid(row = 0, column = 0, padx = 10, pady = 10)
  ttk.Label(window, text = "Password : ").grid(row = 1, column = 0, padx = 10, pady = 10)
  ttk.Entry(window, textvariable = user_id).grid(row = 0, column = 1, padx = 10, pady = 10)
  ttk.Entry(window, textvariable = password, show = '*').grid(row = 1, column = 1, padx = 10, pady = 10)
  ttk.Button(window, text = "Login", command = check_data).grid(row = 2, column = 1, padx = 10, pady = 10)
  ttk.Button(window, text = "Move to Sign up page", command = append_data).grid(row = 2, column = 0, padx = 10, pady = 10)
  
  window.mainloop()
