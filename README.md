## 🗂️ Repository 구성

* 각 *.zip 파일 내 josn, mb, fbx 파일로 구성되어 있음.
  * *.json : 디지털 휴먼 얼굴 근육 변수들 + *.mp3의 각 wave에 해당하여 활성화되는 근육변수와 세기 값이 저장된 파일
  * *.mb : maya를 통해 세부 수정한 얼굴 애니메이션 파일 (중간 작업물)
  * *.fbx : 수정이 최종완료된 *.mb를 export 기능으로 mb>fbx 전환한 파일. UE4 내에서 쓰이는 애니메이션 파일형식.(최종 작업물)
* load_bs_weights_mh_rig_maya.py : maya내에 *.json파일을 읽어와 애니메이션으로 구현하기 위한 파일.

<br>

## 😁 Face Animation 제작과정

![image](https://user-images.githubusercontent.com/57169754/224006629-5f54a05f-5b64-493c-8f3d-3abec0765d3c.png)<br>① 미리 작성한 디지털 휴먼의 대사(text)를 'Naver CLOVA Dubbing'을 통해 mp3파일로 변환한다.

![image](https://user-images.githubusercontent.com/57169754/224007250-7f4ff25a-6c16-44ca-94ee-21fabc2d9674.png)<br> ② 변환된 mp3 파일을 'NVIDIA Omniverse Audio2Face'를 이용하여 디지털휴먼의 Face Animation으로 전환한다. <br>이 단계에서 *.json파일과 load_bs_weights_mh_rig_maya.py파일이 생성된다. (파일에 대한 설명은 위 Repository구성 참조.)
- [Omniverse Audio2Face - How it works?](https://www.nvidia.com/en-gb/omniverse/apps/audio2face/)

![image](https://user-images.githubusercontent.com/57169754/224010236-90d4a14c-3212-46ee-81ac-bc2212f422a1.png)<br>③  load_bs_weights_mh_rig_maya.py파일을 통해 이전단계에서 얻었던 json을 요청하여 Maya로 디지털휴먼 애니메이션을 import 해온다.
- 이는 한국어 mp3를 변환 시킨 애니메이션임에도 영어발음에 맞춰 생성되었기 때문에 입모양이 어색하다. 또한, 눈 깜빡임, 발화 시 얼굴 주변 근육/눈썹 움직임, 영업용 미소도 구현하여 인간다움을 주어야한다. <br>따라서, Maya 내에서 세부수정 작업을 한다.
- 세부수정 작업을 여러번 거치기 때문에 중간 작업물인 *.mb파일이 생성된다.

![image](https://user-images.githubusercontent.com/57169754/224014333-9daea5d8-d089-468c-af2d-95bdb0e534f7.png) <br>④ 최종 수정을 마친 *.mb를 *.fbx로 export하여 언리얼엔진에서 사용할 수 있도록 한다.
<br>

![image](https://user-images.githubusercontent.com/57169754/224016219-6deabffb-6efb-4fe0-83a6-e6374d17c85f.png)<br> ⑤ *.fbx를 UE4내의 Sequencer 기능을 통해 Animation Sequce로 구워 **Dialogue System**에 등록할 수 있도록 한다.
- **Dialogue System**은 이 Kiosk 프로그램의 메인 시스템이며, 상황에 맞는 Animation 및 Audio, 기능을 출력하고 DB조회/저장 등을 수행 하는 시스템이다.

번외) <details>
<summary> 🪄 하다가 접었지만 굉장히 기깔나는 Face Anim 구현방법</summary>

<!-- summary 아래 한칸 공백 두어야함 -->
## 접은 제목
⚠️ 한국어 발화 애니메이션으론 부적합.-> 그래서 하다가 접었다..
</details>

<br>

## 🤸‍♂️ Body Animation 제작과정
![image](https://user-images.githubusercontent.com/57169754/224227003-152b156a-00e8-4bf6-bc2c-a9a7df707989.png)
![image](https://user-images.githubusercontent.com/57169754/224228689-52cb5293-943c-47a5-b3ba-0ab2135e0569.png)
![image](https://user-images.githubusercontent.com/57169754/224228821-d3715147-c98f-499e-9d31-4869d92d2b99.png)
![image](https://user-images.githubusercontent.com/57169754/224228094-873f770d-b104-4187-a175-59b314478205.png)


<br>

## UE4 - Dialogue System 내 Animation 적용과정

<br>

## 역할
|이름|역할|
|------|---|
|안소라|08~13 Face Animation 세부수정|
|임혜진|Face/Body Animation 생성 및 세부수정<br>프로그램 내 Animation 적용|
