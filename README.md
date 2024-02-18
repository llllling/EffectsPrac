# 이펙트 연습
슈리켄으로 만드는 유니티 게임 이펙트 입문 책을 읽고 실습 및 정리

## 게임에서의 이펙트란 ?
### 게임 이펙트의 종류
* 이펙트는 캐릭터 이외의 움직이는 모든 "효과"를 의미한다.
* RPG 게임에서 사용되는 공격, 히트, 회복, 마법 사용 이펙트 등 => 플레이어에게 지금 무언가가 일어나고 있다 등의 상황을 효과적으로 전달
* 게임 내부의 환경을 나타내는 것도 있다 => 비, 눈, 번개, 구름, 안개와 같은 날씨/ 나비처럼 화면에서 움직이는 대부분의 것들이 이펙트이다.
### 게임 이펙트 표현의 폭
* 크게 두 종류로 나눌 수 있다.
* 현실 세계에 있는 현상
    * 날씨 또는 흩날리는 벚꽃 등
* 상상 속의 세계에만 있는 현상
    * 회복, 공격 마법 이펙트
### 이펙트의 외형
* 실루엣, 디테일, 색 3가지 요소가 멋진 이펙트를 만들 때 중요하다.
#### 실루엣
* 이펙트가 어떠한 형태를 하고 있고, 어떠한 움직임을 하는지를 나타내는 것
* 예를 들어 화염에서 타오르는 불꽃, 빛, 연기의 움직임 등
#### 디테일 
* 표현하고 싶은 이펙트를 더 현실적으로 보이게 만들기 위한 세부적인 사항 
* 예로 화염에서 튀어 오르는 불똥
#### 색
* 글자 그대로 대상의 색
### 이펙트의 움직임
* 발생 -> 연출 -> 소멸
#### 발생
* 이펙트가 출현하는 시점을 의미
* 표현하고 싶은 이펙트가 조금씩 나타나거나, 순간적으로 나타나거나, 불타오르면서 나타나거나, 확대되면서 나오는 등의 다양한 표현 방법이 있다.
#### 연출
* 이펙트의 효과를 표현하는 시간
#### 소멸
* 이펙트가 사라지는 것을 의미
* 순간적으로 사라지거나, 긴 시간을 두고 사라지거나, 축소되면서 사라지거나 하는 것처럼 다양한 표현 방법이 있다.

## 파티클 시스템이란?
* 유니티에는 파티클 시스템이라는 표준 파티클 시스템 컴포넌트가 있다.
* 이를 통해 불꽃, 불, 바람, 번개, 마법 등의 다양한 이펙트를 구현할수 있다.
* 주요 설정 항목[https://www.notion.so/Particle-System-Object-1a27e0671aa94d21826da6bac82b04e0?pvs=4]

## 텍스처와 머터리얼 설정
### 텍스처 
* 파티클에서 뿜어져 나오는 이미지를 나타냄
* 텍스처는 다양한 소프트웨어를 사용해서 만듬
    * 포토샵, 애프터 이펙트, 마야, 3ds 맥스 
### 머터리얼
* https://www.notion.so/Material-b2b35e7c0a8b44ebbc6dea3cc26f0c58?pvs=4
* 재질 또는 질감을 의미
* 이펙트에서 머터리얼이라 하면 가산 반투명 머터리얼, 감산 반투명 머터리얼, 반투명 머터리얼, 불투명 머터리얼을 나타내는 경우가 대부분임.
    * 가산 반투명 머터리얼 : 렌더링할 그림을 가산(색을 추가해서 밝게 만듦)하는 설정이다.
    * 감산 반투명 머터리얼 : 렌더링할 그림을 감산(색을 빼서 어둡게 만듦)하는 설정이다.

## 자연 표현 이펙트 연습
NatureEffects 폴더
### 프로젝트 진행하면서 알게 된 것들 
#### Sorting Fudge 속성
* 파티클들의 렌더링 순서를 조절하는 속성.
* 숫자가 작을수록 화면의 앞에 렌더링 된다.
* 예를 들어, 반투명(Alpha Blended) 머터리얼에 Sorting Fudge 값을 "0"으로 설정한 *파티클A*와 Sorting Fudge 값이 "1"인 *파티클B*가 씬 내부에 있다면, *파티클A*가 *파티클B*보다 앞에 렌더링 됨.
    * 앞에 렌더링 됨 == 화면에서 보면 앞에 출력됨
    * 참고로 모두 가산(Additive) 머터리얼을 사용하면 Sorting Fudge를 바꿔도 파티클의 외관에 큰 차이 없음!
    * 따라서 <span style="color: black; background-color:yellow;">반투명 머터리얼로 만든 머터리얼은 Sorting Fudge 설정으로 렌더링 순서를 설정하는 것이 굉장히 중요함.</span>
#### Render Mode
* Render 모듈의 Render Mode를 사용하면 파티클의 형태를 설정할 수 있다.
* 일반적으로 Billboard와 Stretched Billboard만으로도 다양한 이펙트를 표현할 수 있다.
<table>
    <tr>
        <th>선택지</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>Billboard</td>
        <td>항상 카메라 방향을 향하는 정사각형 모양의 폴리곤</td>
    </tr>
    <tr>
        <td>Stretched Billboard</td>
        <td>크기를 변경할 수 있는 사각형 폴리곤. 직사각형의 외형을 만들 때 사용함.</td>
    </tr>
    <tr>
        <td>Horizontal Billboard</td>
        <td>XZ축과 평행한 방향의 사각형 폴리곤</td>
    </tr>
    <tr>
        <td>Vertical Billboard</td>
        <td>Y축과 방향으로 똑바로 서서 항상 카메라를 향하는 사각형 폴리곤</td>
    </tr>
    <tr>
        <td>Mesh</td>
        <td>지정한 3D모델을 파티클로 사용함</td>
    </tr>
</table>

* Stretched Billboard 속성
    * 충격파, 히트 효과, 빛줄기, 불꽃 등의 가느다란 외형의 이펙트를 표현할 때 유용하게 사용할 수 있는 설정임.
    * 하지만 꽤나 다루기 힘든 속성이라 잘 다루려면 반복 조정과 경험이 필요함.
    * Main 모듈의 Start Speed, Start Size를 변경하거나, Shape 모듈의 Radius를 변경하거나, Size over Lifetime 커브 등의 여러 속성을 함께 변경하면서 원하는 외형을 잡아라.
<details>
<summary><h2> 화염 이펙트 </h2></summary>
<div>
화염 이펙트를 제작하면서 조절한 값들 정리

### 1. fire1_add(화염)
#### 텍스처 임포트 설정(eff_aura1.png)
* Alpha Is Transparency > ON  : 투과와 비투과 부분의 경계에서 발생하는 노이즈를 줄여준다. 또한 섬네일 표시가 투과 이미지로 표시됨.
* Wrap Mode > Clamp : 텍스처를 타일 위에 반복할 필요가 없다면 데이터를 가볍게 하기 위해 Clamp로 설정
#### 머터리얼 설정 확인(eff_aura1_add)
* Mobile/Particles/Additive
#### 파티클 시스템에 머터리얼 설정
* Render 모듈의 Material 속성에 eff_aura1_add 할당.
#### Main 모듈
* Start Lifetime
* Start Speed
* Start Size
* Start Rotation
* Gravity Modifier
* *Gravity Modifier을 제외한 값들 임의 범위로 설정함.*
##### 꿀팁
* 임의 범위 설정 : 이펙트의 다양한 성질을 무작위로 설정하면 더 자연스럽고 멋진 표현을 만들 수 있다. 무작위로 설정하면 단조로움을ㅇ 피할 수 있고, 움직임 자체도 자연스럽게 만들 수 있음.
    * 무작위로 설정하려면 각 항목 오른쪽에 아래를 향한 화살표 아이콘을 클릭하고 [Random Between Two Constants]로 변경하면 됨.
* 중력과 역중력
    * 파티클의 감속을 자연스럽게 표현할 수 있다. 
#### Emission 모듈
* Rate > Time > 40  : 1초 동안 40개의 파티클을 방출함.
#### Shape 모듈
* Radius > 0.15 : 방출 범위를 조금 작게 변경함.
#### Rotation over Lifetime 모듈
* Angular Velocity > Random Between Two Constants 
#### Transform 설정
*  Rotation : 파티클을 위로 향하게 Transform을 변경해서 각도를 변경함.
#### Color over Lifetime 모듈
* Color 포인트 4개 추가해서 그레이디언트 만듬 > 색상 사각형 왼쪽 아래에 있는 포인트 아이콘
* 페이드인/페이드아웃 설정 > 색상 사각형 왼쪽 위에 있는 포인트 아이콘(Alpha 값 변경)
##### 꿀팁
* 그레디언트에서 중요한 것
    * 화염 이펙트를 만들 때는 [밝은 노란색] > [노란색] > [주황색] > [붉은색]으로 색을 표현함.
    * 이펙트를 만들 때는 항상 표현하려는 대상의 색상이 어떻게 변화하는지 참고 동영상 또는 사진을 고나찰해야 한다. 그레이디언트를 잘 만들수록 더 사실적인 이펙트를 만들 수 있음
#### Size over Lifetime 모듈
* size > 커브 편집 화면 열기(Inspector 뷰 맨 아래 부분에 [Particle System Curves] 클릭)
* 커브 표현 : 커브로 설정할 수 있는 것은 수명, 크기, 회전, 파티클의 발생 개수 등이 있음.
    * Size over Lifetime 모듈의 Size 커브를 위아래로 크게 변하게 만들면 빛이 반짝이는 효과를 만들 수 있다.
    * Emission 모듈의 Rate를 오른쪽 위로 오르는 커브로 만들면 파티클의 발생 개수가 점점 늘어나게 만들 수 있음.
### 2. par1_add(불똥)
#### 머터리얼 설정 확인(eff_par1_add)
* Mobile/Particles/Additive
#### 파티클 시스템에 머터리얼 설정
* Render 모듈의 Material 속성에 eff_par1_add 할당.
#### Main 모듈
* Start Lifetime
* Start Speed
* Start Size 
* Gravity Modifier 
#### Emission 모듈
* Rate > Time > 100 : 1초동안 100개의 파티클을 방출
#### Shape 모듈
* Angle > 20 : 방출 각도 조금 작게 변경 
* Radius > 0.2 : 방출 범위를 조금 작게 변경
#### Color over Lifetime 모듈
* fire1_add의 Color over Lifetime 모듈의 Color 클릭 > Presets [New] 클릭 > 그레이디언트 프리셋이 생서됨.
* par1_add를 선택하고 Color over Lifetime 모듈의 Color를 위에서 생성한 Presets 그레이디언트 클릭해서 복사함.
#### Size over Lifetime 모듈
* Particle System Curves에서 오른쪽 아래로 내려가는 직선을 선택한다 > 파티클이 점점 작아지는 이펙트가 됨.

### 3. smoke1_alpha(연기)
#### 텍스처 임포트 설정(eff_smoke1.png)
* Alpha Is Transparency > ON
* Wrap Mode > Clamp
#### 머터리얼 설정 확인(eff_smoke1_alpha)
* Mobile/Particles/AlphaBlended
#### 파티클 시스템에 머터리얼 설정
* Render 모듈의 Material 속성에 eff_smoke1_alpha 할당.
#### Main 모듈
* Start Lifetime
* Start Speed
* Start Size
* Start Rotation
* Gravity Modifier
* Start Color
#### Emission 모듈
* Rate > Time
#### Shape 모듈
* Radius
#### Rotation over Lifetime 모듈
* Angular Velocity > Random Between Two Constants
#### Color over Lifetime 모듈
* fire1_add를 기반으로 복사한 Presets의 색상 그레이디언트 사용
* 연기는 연소된 후에 남는 것이므로 이런 것을 표현하기 위해> 복사한 그레이디언트의 제일 오른쪽 Color를 (70, 0, 0)으로 변경
#### Size over Lifetime 모듈
* Particle System Curves에서 오른쪽 위로 향하는 직선을 선택한다. 왼쪽에 있는 키를 드래그해서 0.600 위치로 옮김 > 점점 커지게 
</div>
</details>

<details>
<summary><h2> 물 이펙트 </h2></summary>
<div>

### 1. water1_add(물)
물보라가 강하게 위로 발생한 뒤 낙하하며 사라지는 이펙트
#### 파티클 시스템에 머터리얼 설정
* Render 모듈의 Material 속성에 eff_water1_add 할당.
#### Main 모듈
* Start Lifetime
* Start Speed
* Start Size
* Start Rotation
* Gravity Modifier
#### Emission 모듈
* Rate > Time
#### Shape 모듈
* Angle : 물보라가 너무 넓게 퍼지므로 방출 각도를 줄인다.
* Radius : 물보라가 너무 넓게 퍼지므로 방출 범위를 줄인다.
#### Rotation over Lifetime 모듈
* Angular Velocity : 물보라가 너무 단조로우므로 무작위로 회전시킨다.
#### Transform 설정
*  Rotation > (-90, 0, 0) : 옆으로 낙하하던 것을 위로 향하게
#### Color over Lifetime 모듈
* 밝은 하늘색 > 하늘색 > 파란색 그레이디언트 만들기
* 페이드아웃해서 사라지도록 Alpha 조정
#### Size over Lifetime 모듈
* Particle System Curves에서 오른쪽 위로 향하는 직선을 선택한다. 왼쪽에 있는 키를 드래그해서 0.350 위치로 옮김  
    * 물보라 파티클이 생성될 때는 작고, 시간이 경과하면 점점 커지도록.
    * 즉, 물보라가 낙하하면서 점점 커지고, 사라지게 된다.
### 2. smoke1_alpha(물안개)
#### 파티클 시스템에 머터리얼 설정
* Render 모듈의 Material 속성에 eff_smoke1_add 할당.
* Sorting Fudge > 50 : 가산 표시 물체보다 뒤에 렌더링 해야 하므로
#### Main 모듈
* Start Lifetime
* Start Speed
* Start Size
* Start Rotation
* Gravity Modifier
* Start Color
#### Emission 모듈
* Rate > Time
#### Shape 모듈
* Angle : 물안개가 너무 넓게 퍼지므로 방출 각도를 줄인다.
* Radius : 물안개가 너무 넓게 퍼지므로 방출 범위를 줄인다.
#### Rotation over Lifetime 모듈
* Angular Velocity : 물안개가 너무 단조로우므로 무작위로 회전시킨다.
#### Transform 설정
*  Rotation > (-90, 0, 0) : 옆으로 낙하하던 것을 위로 향하게
#### Color over Lifetime 모듈
#### Size over Lifetime 모듈
* Particle System Curves에서 오른쪽 위로 향하는 직선을 선택한다. 왼쪽에 있는 키를 드래그해서 0.350 위치로 옮김  
    * 물안개 파티클이 생성될 때는 작고, 시간이 경과하면 점점 커지도록.
    * 즉, 물안개 낙하하면서 점점 커지고, 사라지게 된다.
</div>
</details>

<details>
<summary><h2> 폭포 이펙트 </h2></summary>
<div>

### 1. water1_add(폭포)
#### 파티클 시스템에 머터리얼 설정
* Render 모듈의 Material 속성에 eff_water1_add 할당.
#### 파티클 그래픽 이미지를 직사각형으로 변경
* Render 모듈 > Render Mode > Stretched Billboard로 설정 > Length Scale 2로 변경 => Billboard가 조금 길어짐
#### Main 모듈
* Start Lifetime
* Start Speed
* Start Size
* Gravity Modifier
#### Emission 모듈
* Rate > Time > 200 : 발생량을 늘려서 물보라를 강하게 만든다.
#### Shape 모듈
* Angle  : 물보라가 너무 넓게 퍼지므로 방출 각도를 줄임.
* Radius : 물보라가 너무 넓게 퍼지므로 방출 범위를 줄임.
#### Color over Lifetime 모듈
#### Size over Lifetime 모듈
* Particle System Curves에서 오른쪽 위로 향하는 직선을 선택한다. 왼쪽에 있는 키를 드래그해서 0.77 위치로 옮김  
    * 물보라 파티클이 생성될 때는 작고, 시간이 경과하면 점점 커지도록.
    * 즉, 낙하하면서 점점 커지고, 사라지게 된다.
### 2. smoke1_alpha(물안개)
#### 파티클 시스템에 머터리얼 설정
* Render 모듈의 Material 속성에 eff_smoke1_add 할당.
* Sorting Fudge > 50 : 가산 표시 물체보다 뒤에 렌더링 해야 하므로
#### Main 모듈
* Start Lifetime
* Start Speed
* Start Size
* Start Rotation
* Gravity Modifier
* Start Color
#### Emission 모듈
* Rate > Time
#### Shape 모듈
* Angle 
* Radius
#### Rotation over Lifetime 모듈
* Angular Velocity : 물안개가 너무 단조로우므로 무작위로 회전시킨다.
#### Color over Lifetime 모듈
#### Size over Lifetime 모듈
* Particle System Curves에서 오른쪽 위로 향하는 직선을 선택한다. 왼쪽에 있는 키를 드래그해서 0.77 위치로 옮김  
</div>
</details>