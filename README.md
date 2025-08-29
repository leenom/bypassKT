
# bypassQoSKoreatelecomISP

## ROKFOSS 프로젝트에서 일부 수정하였습니다

이 글은 ROKFOSS 프로젝트에서 일부 수정한 것입니다. [원본](https://github.com/veilRedeemer/bypassQoSKoreatelecomISP)에는 없는 부분이 있을 수 있습니다.

아래 방법은 KT 사용자들에게만 유효하며 LGU+ 및 SKB는 사용할 수 없습니다. LGU+ 경우 현재까지 알려진 방법은 없습니다. 만약 우회가 필요하다면 KT 또는 SKB(대칭형)으로 인터넷을 바꾸는 것도 방법이 될 수 있습니다.

ROKFOSS 프로젝트에서 추가한 부분에 대해서 문의가 있거나 새로운 정보가 있다면 krfoss@krfoss.org로 문의하거나 [ROKFOSS 커뮤니티](https://chat.krfoss.org)에서 사람들과 정보를 교류해보세요! 이곳에는 없는 방법들을 함께 연구할 수 있습니다.

설정이 제대로 되었는지 확인하고 싶다면 ROKFOSS 프로젝트 분산미러 웹 사이트를 [방문](https://http.krfoss.org)하여 자신의 위치 정보를 확인하세요. 위치가 한강에 빠져있다고 나온다면 설정이 올바르게 된것입니다.

> [!TIP]
> 이 글은 네트워크 장비에 관한 지식이 필요합니다. 관련한 지식이 부족하거나 없는 경우에는 구글 검색이 유용할 수도 있습니다. 또는 인공지능의 도움을 받는 것도 방법이 될 수 있지만 인공지능의 환각으로 인한 잘못된 정보를 받을 수 있습니다.
> > KT뿐만 아니라 KT 계열사(KT망을 이용하는) 일부 서비스 제공업체에서도 이러한 설정을 적용하여 사용할 수 있습니다.
> > 
> > 확인됨 : KT 스카이라이프

> [!TIP]
> 설정이 제대로 되었는지 확인하고 싶다면 ROKFOSS 프로젝트 분산미러 웹 사이트를 [방문](https://http.krfoss.org)하여 자신의 위치 정보를 확인하세요. 위치가 서울 한강에 빠져있다고 뜬다면 잘 된것입니다.

## TPLINK ROUTER

2025년 5월에 나온 최신 펌웨어를 적용하면 TP-Link 라우터에서 Option 60을 사용할 수 있습니다. ER605 모델을 기준으로 설정 방법은 다음과 같습니다:

1.  **라우터 관리자 페이지에 접속**한 후 로그인합니다.    
2.  좌측 메뉴에서 **Network** 탭을 선택하고 **WAN**으로 들어갑니다.
3.  **WAN1**을 선택한 후, **Advanced Settings**를 클릭합니다.
4.  탭이 열리면 **Option 60** 항목에 아래 값을 입력합니다:
    ```
    KT_PR_HH_A_A
    ```
5.  입력 후, **Save**를 클릭하여 설정을 저장합니다.

**참고:** 다른 TP-Link 라우터나 공유기에서 Option 60을 성공적으로 설정한 사례가 있다면, [krfoss@krfoss.org](mailto:krfoss@krfoss.org)로 이메일을 보내주세요.

## OPNsense

OPNsense에서 WAN 인터페이스에 Option 60을 추가하려면 다음과 같은 절차를 따르세요:

1.  **Interfaces 탭**에서 **WAN 인터페이스**를 선택합니다.
2.  **DHCP Client Configuration** 섹션에서 **Configuration Mode**를 **Advanced**로 변경합니다.
3.  **Lease Requirements** 항목 아래의 **Send Options** 입력란에 `dhcp-class-identifier "KT_PR_HH_A_A"` 를 입력합니다.
4.  변경 사항을 완료한 후, **Save** 버튼을 클릭하여 저장합니다.

이렇게 하면 WAN 인터페이스에 Option 60을 성공적으로 추가할 수 있습니다.

<img width="900" height="1060" alt="image" src="https://github.com/user-attachments/assets/3b6051b2-1058-4d6e-a7f6-25ec6a0d558b" />

## MikroTik(미크로틱 라우터)

예시 사용기기: MikroTik Hap AX3(C53UiG+5HPaxD2HPaxD)

<img width="575" height="726" alt="Image" src="https://github.com/user-attachments/assets/2704f43a-06bf-420f-ab66-77005a3cd93c" />

1. WinBox 접속후 우측 메뉴에서 IP -> DHCP Client로 이동.

<img width="766" height="467" alt="Image" src="https://github.com/user-attachments/assets/bb6cdd37-e5ba-4680-8e7b-c2928cadda2c" />

2. 상단 메뉴인 DHCP Client Options 로 진입 이후 이미지와 같이 설정. (단 value 값은 **반드시 작은따옴표**로 감싸야 함)

| 항목 | 값 |
| ------------- | ------------- |
| Name  | 사용자 마음대로  |
| Code | 60  |
| Value | 'KT_PR_HH_A_TNIE_TI04-708H' (예시)  |

<img width="1144" height="673" alt="Image" src="https://github.com/user-attachments/assets/9bcc4575-72e2-4066-878b-720a306240ed" />

3. 2번에서 지정한 메뉴 옆의 DHCP Client를 눌러준 뒤 사용중인 인터페이스 클릭.

이후 상단의 Advanced 메뉴로 진입 후 DHCP Options에 2번에서 설정한 타입 지정 후 저장. (이미지 참고)



이후에 라우터를 재부팅 하면 IP가 KT 프리미엄 IP로 변경 됩니다.

# 아래부터는 ROKFOSS 프로젝트에서 관리하지 않는 부분입니다.

> [!WARNING]
> 가정용 공유기는 [원본](https://github.com/veilRedeemer/bypassQoSKoreatelecomISP) 문서에서 확인하실 수 있습니다.


## KT GiGA WiFi (통신사 Router, 기본값 설정인 KT 모드가 필요)
제한에서 벗어날 <ins>**각 기기**</ins>(이중 NAT 구성의 미지원 Router 포함)에 대해 수동IP설정 **또는** GiGA WiFi의 사용자 설정 웹 페이지에서 '수동 IP 할당 설정'(DHCP 정적 할당) 설정을 마치세요

아래 표를 확인하여 현재 사용중인 모델의 KT GiGA WiFi에서 사용 가능여부(추측 포함)를 확인하기\:

|＼|수동IP설정|수동 IP 할당 설정|업그레이드,TR069 차단|
|---------:|:--|:--|:--|
|KM06-506H, KM06-704H|？|✕|？|
|DW02-412H|？|✕|✕|
|KM08-708H, DV01-901H<br>Wave2|？|？|？|
|TI04-708H Wave2|〇|✕|✕|
|KM12-007H<br>GiGA WiFi home ax|？|？|？|
|KM17-305H<br>GiGA WiFi home ax|〇|〇|？|
|KM15-103H<br>GiGA WiFi home ax|〇|〇|〇|
|DV02-012H<br>GiGA WiFi home ax|〇|〇|✕|
|HR08-407H<br>GiGA WiFi home ax|〇|✕|〇|
|AR06-012H<br>GiGA WiFi home ax|〇|✕|✕|
|KM18-311H<br>KT WiFi 6D|？|？|？|
|KB01-411H<br>KT WiFi 7D|？|？|？|

__표에서 확인할 수 없는 모델의 각 기능 사용 가능여부를 여러분의 제보(Issues, 메일주소 3570kgen@naver.com , 기여자에 대한 기록을 남기고 싶을경우 Pull Request 등)를 통해 보충할 수 있게 해주세요!__

__사용중인 기기의 모델명, 펌웨어 버전, 수동IP설정, '수동 IP 할당 설정'의 성공 여부,__
__KT GiGA WiFi 사용자 설정 페이지 - 상태정보의 로그('Update' 또는 'Upgrade' 등의 문자열을 포함하는 로그 확인, 부팅 후 많은 시간이 지나면 다른 로그에 의해 확인할 수 없는 경우가 있음)를 확인한 후, 'Update' 또는 'Upgrade' 등의 문자열을 포함하는 로그가 아래의 4가지 규칙 추가 & 재부팅 후 2-5분 후에 기록되는 로그와 비교해 차이점이 있는지 확인하고 알려주셨으면 합니다.__

-

--------------------------------
