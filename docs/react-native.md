# REACT-NATIVE  

 - 페이스북에서 만든 오픈 소스 모바일 응용 프로그램.(크로스 플랫폼)
 - 네이티브코드-> js번들 -> 브릿지 -> Native thread
                        -> Js thread
 - 번들만드는방법
  1. Expo CLI
    - 장점
      - 개발환경 구축 용이/실제 개발이 쉽고 편함
    - 단점
      - OS 레이어와 직접 상호작용 불가능(Java, Kotlin, Obj-C, Swift로 추가 작성불가)
      - Expo에서 제공해주는 모듈만 사용가능
      - Expo Client에서는 잘동작하지만 실제 시뮬레이터 및 단말기에서는 동작 하지않을 수있음.
      - 개발관점에서 `자유도가 낮음`
  2. React Native CLI(choice)
      - 장점
        - Expo로는 접근하지 못하는 Native 기능 접근가능(Native모듈 사용 자유도 높음)
        - 원하는 언어로 추가 작성 가능(커스텀 네이티브 모듈 사용가능)
        - 필요한 기능이 있는 경우 모듈 직접 제작가능
        - OS Layer와 직접 상호작용 가능
      - 단점
        - 초기 개발환경 구축 및 실제 앱 개발 시간 소요
        - Mac일 경우에만 안드/ios지원

  - 환경구축
    - nvm(node 버전 매니저)
    - nodejs
    - npm(node package manager)
    - 안드로이드 스튜디오 -Android Debug Bridge version 1.0.41 adb
    - 자바
    - XCode -> mac에서설치가능 ios용프로그램
    - vscode
    - cocoapod -> mac에서설치가능 ios용프로그램
    - React native cli

  - 새프로젝트 생성

    - react-native init --version 0.61.5 [프로젝트명] 설치  프로젝트명 대쉬(-)사용불가

  - 안드/IOS 에뮬레이터 사용법
    - ios
      1. npm start
      2. react-native run-ios (새로고침 cmd +r, cmd + d 디버깅)
      3. react-native run-ios --simulator="iPhone 8 Plus" (다른 모델 버전 구동시 )
    - android
      1. android 에뮬레이터 실행 후
      2. react-native run-andorid (r 새로고침, cmd +m 디버깅)


    -  bash_profile 환경변수적용
       -  source ~/.bash_profile


  - View
    - 화면을 채우는 컨테이너 같은 역활. <div> 와비슷.
    - 높이나,길이,마진등 사용시 소숫점사용불가

  - style 
    - inline방식
    - StyleSheet 활용하여 클래스로 지정

  - touch Event
    - TouchableOpacity - View바깥을 해당 태그로 감싸서 이벤트를 추가
      - onPress
      - onLongPress - 길게눌러야 이벤트발생
      - onPressIn - 누르자마자 바로반응.
      - onPressout - 터지가 떨어질때 이벤트발생.
    - TouchalbeWidthFeedback - 클릭이벤트 발생시 투명해지는효과가 X
      - 스타일이먹지 안먹기때문에 VIEW에적용해야함.
    - Text에도 onPress가능

  - Button
    - title 속성 필수 
    - onPress 이벤트.
  - ScrollView (V)
    - 화면박으로 컴포넌트 넘어갓을때사용
    - 넘어가는 컴포넌트를 ScrollView 컴포넌트사이에 넣기
    - onMomentumScrollBegin 이벤트 : 스크롤 이동후 놓을때 이벤트발생
    - onMomentumScrollEnd
    - onScroll : 스크롤움직임 발생할때 trigger해줌.
    - onContentSizeChange : 스크롤뷰의 사이즈변동시 발생 (width, height) =>{}
    - bounces={true} : 스크롤후 통통튀는 기능.(디폴트 true)

  - TextInput
     - value: TextInput 입력값을 가져옴
     - onChangeText: 택스트변경시 호출.
     - multiline={true} : 글자수 길어질때 개행해줌
     - maxLength : 입력값 길이제한
     - autoCapitalize={'none'} : 앞글자 대문자 자동수정 방지
     - editable : 수정가능하게

  - Picker
      - 콤보박스처럼 여러값중 고르는기능
      - React-native community 에서 picker 설치
      - Picker 안에 <Picker.item label="" value="" />->select의 option 과 비슷
      - selectedValue를 지정해서 해당 선택된 값이 먼지 알수잇따.
      - onValueChange={(val, idx) =>{}}

  - `React-native community 깃헙 !!! -필요한것들 다운받아사용`
  
  -  Slider
     -  npm install @react-native-community/slider --save
     -  cd ios -> npx pod-install
     -  props
        -  value:초기값
        -  minimumValue: 최소값
        -  maximumValue: 최대값
        -  onValueChange: (value)=>{setState({값})}
        -  minimumTrackintColor: 최소값쪽 슬라이더 바 컬러
        -  maximumTrackintColor: 최대값쪽 슬라이더 바 컬러
        -  step: 몇단위로 슬라이드될것인지 설정

  -  ActivityIndicator(react-native 모듈)
     - size: "large"
     - color: 색상선택
     - animating: true
  
  - Image (react-native 모듈)
    - source : 경로설정 or 임포트로 이미지가져오기 or {uri:'url경로'}
    - style 설정
    - resizeMode: cover,contain,stretch,repeat,center
    - onLoadEnd: 이미지로딩이 끝낫후 트리거 해주는 이벤트

  - Modal
    - props
      - visible: true일때 모달 활성화
      - animationType
        - none, slide, fade
      - onShow: 모달이 보여질때 발생하시는 이벤트