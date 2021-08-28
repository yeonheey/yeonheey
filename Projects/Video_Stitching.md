# Video Stitching <br/>

## 프로젝트 개요
두 개의 비디오 영상을 'image stitching' 원리를 통해 두 영상을 매칭 및 결합하여 하나의 영상을 도출합니다.
* 이미지스티칭이란? <br/>
넓은 시야의 이미지를 생성하기 위해 다중의 영상을 정합하는 방법 
<br/><br/>

## 프로젝트 기능
openCV framework를 사용해 영상을 스티칭합니다.
* C++를 활용해 openCV를 사용했으며 SURF 알고리즘을 사용하기 위해 github_contrib를 사용했습니다.
* openCV에서 이미지 스티칭 기능을 제공하는 stitcher를 사용하지 않고 파노라마 이미지를 만드는 과정을 이해하기 위해 직접 구현합니다.
* 비디오 프레임 별 feature points이 달라지기 때문에 homography 계산 결과가 달라 영상이 불안정해지는 것을 막고자 한 쌍의 프레임에서 homography를 계산하여 모든 프레임에 적용시켰습니다.
* 스티칭한 결과 영상에서 이음새 부분이 부자연스러운 것을 해결하고자 blending(멀티 블렌딩)을 적용해 이음새를 부드럽게 만들었습니다.
* 또한, 결과 영상에서 테두리 부분의 검은색 잔여 영역을 Rect()을 활용하여 잘라냈습니다.
<br/> <br/>

### Homography
*  Homography란? <br/>
한 평면을 다른 평면에 투영시킬 때, 투영된 대응점들 사이에 일정한 변환관계입니다.

openCV에서 제공하는 homography 함수를 사용하지 않고 ```DLT 알고리즘``` 을 통해 추정했습니다. <br/>

### 이미지 블렌딩
* 가우시안 피라미드를 구축 후 라플라시안 피라미드로 변환해 블렌딩 적업을 거쳐 이미지를 변환 시키는 멀티 밴드 블렌딩을 적용했습니다.
<br/><br/>

## 결과 영상 
### 테스트 영상 전제 조건
1. 동일한 기종의 핸드폰으로 촬영
2. 고정된 위치에서 촬영된 2개의 동영상
3. 두 영상 사이에 30~40% 겹치는 부분이 존재

|left image|right image|
|:----------:|:-----------:|
|<img width="80%" src="https://user-images.githubusercontent.com/50892654/131219151-70b63897-9a9e-4eeb-9f0b-abf504edd263.gif"> | <img width="80%" src="https://user-images.githubusercontent.com/50892654/131219172-2ab5ed2f-4b14-4336-8d6f-c2a067c05097.gif">|
<br/>

### result video
<img width="80%" src="https://user-images.githubusercontent.com/50892654/131219204-f00fd3a9-593b-4f22-9b38-870489d8818b.gif">