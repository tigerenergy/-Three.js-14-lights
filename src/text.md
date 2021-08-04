소개
이전 단원에서 보았듯이 조명을 추가하는 것은 메시를 추가하는 것만큼 간단합니다. 적절한 클래스를 사용하여 라이트를 인스턴스화하고 장면에 추가합니다.

여러 유형의 조명이 있으며 이미 AmbientLight 및 PointLight 를 발견했습니다 .

이 수업에서는 다양한 클래스와 사용 방법에 대해 자세히 알아보겠습니다.

설정
장면은 이미 스타터에 설정되어 있지만(구, 정육면체, 원환체 및 평면을 바닥으로 하여 완성), 연습하고 싶다면 자유롭게 시도해 보십시오.

조명을 사용할 것이기 때문에 조명에 반응하는 재질을 사용해야 합니다. 우리는 사용할 수도 MeshLambertMaterial , MeshPhongMaterial 또는 MeshToonMaterial을 , 대신 우리는 사용 MeshStandardMaterial을 우리가 이전 강의에서 본대로 가장 현실적인 일이기 때문에. 우리는 또한 빛의 반사를 보기 위해 roughness머티리얼을 줄였습니다 0.4.

/assets/lessons/14/step-01.png

스타터가 작동하면 AmbientLight 와 PointLight 를 제거하여 처음부터 시작하십시오. 아무것도 보이지 않는 검은색 렌더를 얻어야 합니다.

앰비언트 라이트
주변 광은 장면의 모든 형상에 전 방향 조명을 적용합니다. 첫 번째 매개변수는 color이고 두 번째 매개변수는 intensity입니다. 재료의 경우 인스턴스화할 때 속성을 직접 설정하거나 다음과 같이 변경할 수 있습니다.

const ambientLight = new THREE.AmbientLight(0xffffff, 0.5)
scene.add(ambientLight)

// Equals
const ambientLight = new THREE.AmbientLight()
ambientLight.color = new THREE.Color(0xffffff)
ambientLight.intensity = 0.5
scene.add(ambientLight)
자바스크립트
/assets/lessons/14/step-02.png

그리고 머티리얼에 대해 했던 것처럼 디버그 UI에 속성을 추가할 수 있습니다. 나머지 강의에서는 그렇게 하지 않겠지만 테스트를 쉽게 하고 싶다면 자유롭게 조정할 수 있습니다.

gui.add(ambientLight, 'intensity').min(0).max(1).step(0.001)
자바스크립트
당신이 가진 모든이 경우 주변 광이 당신은에 대한 것과 같은 효과가 있습니다 MeshBasicMaterial 기하학의 모든면이 동등하게 불이되기 때문입니다.

실생활에서 물체에 불을 붙이면 빛이 벽과 다른 물체에 반사되기 때문에 빛의 반대쪽에 있는 물체의 측면이 완전히 검은색은 아닙니다. 빛 바운스는 성능상의 이유로 Three.js에서 지원되지 않지만 희미한 AmbientLight 를 사용하여 이 빛 바운스를 가짜로 만들 수 있습니다 .

디렉셔널 라이트
DirectionalLight는 태양 광선이 병렬로 여행하는 것처럼 태양과 같은 영향을 미칠 것입니다. 첫 번째 매개변수는 color이고 두 번째 매개변수는 다음과 intensity같습니다.

const directionalLight = new THREE.DirectionalLight(0x00fffc, 0.3)
scene.add(directionalLight)
자바스크립트
/assets/lessons/14/step-03.png

기본적으로 빛은 위에서 오는 것처럼 보입니다. 이를 변경하려면 position일반 오브젝트처럼 속성 을 사용하여 전체 조명을 이동해야 합니다.

directionalLight.position.set(1, 0.25, 0)
자바스크립트
/assets/lessons/14/step-04.png

빛의 거리는 지금은 중요하지 않습니다. 광선은 무한 공간에서 나와 무한 반대 방향으로 평행하게 이동합니다.

반구빛
HemisphereLight는 받는 사람과 유사 주변 광 하지만 지상에서 나오는 색상보다 하늘에서 다른 색으로. 하늘을 향한 면은 한 색상으로 조명되고 다른 색상은 지면을 향한 면에 조명이 켜집니다.

첫 번째 매개변수는 color하늘색에 해당하고 두 번째 매개변수는 groundColor이고 세 번째 매개변수는 다음과 intensity같습니다.

const hemisphereLight = new THREE.HemisphereLight(0xff0000, 0x0000ff, 0.3)
scene.add(hemisphereLight)
자바스크립트
/assets/lessons/14/step-05.png

포인트라이트
PointLight는 거의 가벼운 같다. 광원은 무한히 작고 빛은 모든 방향으로 균일하게 퍼집니다. 첫 번째 매개변수는 color이고 두 번째 매개변수는 다음과 intensity같습니다.

const pointLight = new THREE.PointLight(0xff9000, 0.5)
scene.add(pointLight)
자바스크립트
/assets/lessons/14/step-06.png

다른 개체처럼 이동할 수 있습니다.

pointLight.position.set(1, - 0.5, 1)
자바스크립트
/assets/lessons/14/step-07.png

기본적으로 빛의 강도는 사라지지 않습니다. 그러나 distance및 decay속성을 사용하여 페이드 거리와 페이드 속도를 제어할 수 있습니다. 클래스의 매개변수에서 세 번째 및 네 번째 매개변수로 설정하거나 인스턴스의 속성에서 설정할 수 있습니다.

const pointLight = new THREE.PointLight(0xff9000, 0.5, 10, 2)
자바스크립트
/assets/lessons/14/step-08.png

RectAreaLight
RectAreaLight은 당신이 사진 촬영 세트에 볼 수있는 큰 직사각형 조명처럼 작동합니다. 디렉셔널 라이트와 디퓨즈 라이트의 혼합입니다. 첫 번째 매개변수는 color, 두 번째 매개변수는 intensity, 세 번째 매개변수는 width직사각형, 네 번째 매개변수는 입니다 height.

const rectAreaLight = new THREE.RectAreaLight(0x4e00ff, 2, 1, 1)
scene.add(rectAreaLight)
자바스크립트
/assets/lessons/14/step-09.png

RectAreaLight는 에서만 작동 MeshStandardMaterial 및 MeshPhysicalMaterial .

그런 다음 라이트를 이동하고 회전할 수 있습니다. 회전을 쉽게 하기 위해 lookAt(...)이전 단원에서 본 방법을 사용할 수 있습니다 .

rectAreaLight.position.set(- 1.5, 0, 1.5)
rectAreaLight.lookAt(new THREE.Vector3())
자바스크립트
/assets/lessons/14/step-10.png

Vector3 어떤 매개 변수없이는 것 x, y그리고 z에 0(현장 중심).

스포트라이트
스포트 라이트는 손전등처럼 작동합니다. 한 점에서 시작하여 한 방향으로 향하는 빛의 원뿔입니다. 매개변수 목록은 다음과 같습니다.

color: 그 색깔
intensity: 강도
distance: 강도가 떨어지는 거리 0
angle: 빔의 크기
penumbra: 빔의 윤곽이 얼마나 확산되었는지
decay: 빛이 얼마나 빨리 어두워지는가
const spotLight = new THREE.SpotLight(0x78ff00, 0.5, 10, Math.PI \* 0.1, 0.25, 1)
spotLight.position.set(0, 2, 3)
scene.add(spotLight)
자바스크립트
/assets/lessons/14/step-11.png

SpotLight를 회전 하는 것은 조금 더 어렵습니다. 인스턴스에는 Object3D 라는 속성 target이 있습니다. 스포트라이트는 항상보고있다 객체입니다. 그러나 위치를 변경하려고 하면 SpotLight 가 움직이지 않습니다.target

spotLight.target.position.x = - 0.75
자바스크립트
/assets/lessons/14/step-12.png

그것은 우리 target가 현장에 있지 않기 때문입니다. target장면에 추가하기 만 하면 작동합니다.

scene.add(spotLight.target)
자바스크립트
/assets/lessons/14/step-13.png

성능
조명은 훌륭하고 잘 사용하면 현실적일 수 있습니다. 문제는 성능 면에서 조명 비용이 많이 들 수 있다는 것입니다. GPU는 얼굴에서 빛까지의 거리, 그 얼굴이 빛을 얼마나 향하고 있는지, 얼굴이 스포트 라이트 원뿔 안에 있는지 등과 같은 많은 계산을 수행해야 합니다.

가능한 한 적은 수의 조명을 추가하고 더 저렴한 조명을 사용하십시오.

최소 비용:

앰비언트 라이트
반구빛
적당한 비용:

디렉셔널 라이트
포인트라이트
고비용:

스포트라이트
RectAreaLight
빵 굽기
조명을 위한 좋은 기술을 베이킹이라고 합니다. 아이디어는 빛을 텍스처에 굽는 것입니다. 이것은 3D 소프트웨어에서 수행할 수 있습니다. 불행히도 조명을 움직일 수 없습니다. 조명이 없고 아마도 많은 텍스처가 필요할 것이기 때문입니다.

좋은 예는 Three.js Journey 홈 페이지입니다.

/assets/lessons/14/baked.jpg

도우미
조명을 배치하고 방향을 지정하는 것은 어렵습니다. 우리를 돕기 위해 도우미를 사용할 수 있습니다. 다음 도우미만 지원됩니다.

HemisphereLightHelper
DirectionalLightHelper
PointLightHelper
RectAreaLightHelper
SpotLightHelper
사용하려면 해당 클래스를 인스턴스화하면 됩니다. 해당 조명을 매개변수로 사용하고 장면에 추가합니다. 두 번째 매개변수를 사용하면 도우미를 변경할 수 있습니다 size.

const hemisphereLightHelper = new THREE.HemisphereLightHelper(hemisphereLight, 0.2)
scene.add(hemisphereLightHelper)

const directionalLightHelper = new THREE.DirectionalLightHelper(directionalLight, 0.2)
scene.add(directionalLightHelper)

const pointLightHelper = new THREE.PointLightHelper(pointLight, 0.2)
scene.add(pointLightHelper)
자바스크립트
/assets/lessons/14/step-14.png

를 들어 SpotLightHelper , 더이없는 size매개 변수입니다. 또한 대상을 이동한 후 update(...)다음 프레임 에서 메서드 를 호출해야 합니다 .

const spotLightHelper = new THREE.SpotLightHelper(spotLight)
scene.add(spotLightHelper)
window.requestAnimationFrame(() =>
{
spotLightHelper.update()
})
자바스크립트
/assets/lessons/14/step-15.png

RectAreaLightHelper는 훨씬 더 힘들어 사용하는 것입니다. 현재 클래스는 THREE변수의 일부가 아닙니다 . OrbitControls에서examples 했던 것처럼 종속성 에서 가져와야 합니다 .

import { RectAreaLightHelper } from 'three/examples/jsm/helpers/RectAreaLightHelper.js'
자바스크립트
그런 다음 사용할 수 있습니다.

const rectAreaLightHelper = new RectAreaLightHelper(rectAreaLight)
scene.add(rectAreaLightHelper)
자바스크립트
