# Re:Free - 냉장고 식재료 관리 iOS 앱

<!-- <p align="center">
  <img width="150" alt="1" src="https://github.com/user-attachments/assets/283b7ca0-93b1-4b70-ae5d-a27c7014b36a" />
  <img width="150" alt="2" src="https://github.com/user-attachments/assets/bc3ed7da-8c86-4790-aa55-134f117627f3" />
  <img width="150" alt="3" src="https://github.com/user-attachments/assets/7092925a-eda1-49b9-a938-6c1e9672f9c6" />
  <img width="150" alt="4" src="https://github.com/user-attachments/assets/40c2049e-6f6b-4771-a249-0ccf6a57fc6d" />
  <img width="150" alt="5" src="https://github.com/user-attachments/assets/834ea10f-c3b2-46a9-b93c-94fec1db2274" />
</p> -->

<p align="center">
  <img width="19%" alt="1" src="https://github.com/user-attachments/assets/283b7ca0-93b1-4b70-ae5d-a27c7014b36a" />
  <img width="19%" alt="2" src="https://github.com/user-attachments/assets/bc3ed7da-8c86-4790-aa55-134f117627f3" />
  <img width="19%" alt="3" src="https://github.com/user-attachments/assets/7092925a-eda1-49b9-a938-6c1e9672f9c6" />
  <img width="19%" alt="4" src="https://github.com/user-attachments/assets/40c2049e-6f6b-4771-a249-0ccf6a57fc6d" />
  <img width="19%" alt="5" src="https://github.com/user-attachments/assets/834ea10f-c3b2-46a9-b93c-94fec1db2274" />
</p>

<p align="center">
  <strong>냉장고 속 식재료를 스마트하게 관리하고, 맞춤 레시피를 추천받으세요</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Swift-5.0+-orange.svg" alt="Swift 5.0+"/>
  <img src="https://img.shields.io/badge/UIKit-100%25-blue.svg" alt="UIKit"/>
  <img src="https://img.shields.io/badge/Version-1.0.1-green.svg" alt="Version 1.0.1"/>
</p>

---

## 주요 기능

### 식재료 관리
- 카메라/갤러리를 통한 식재료 사진 등록
- 카테고리에서 식재료 분류
- 보관 방법별 관리 (실온, 냉장, 냉동)
- 유통기한 추적 및 임박 알림
- 수량 및 메모 관리

### 레시피 추천
- 보유 식재료 기반 맞춤 레시피 추천
- 키워드 및 카테고리별 레시피 검색
- 북마크 기능으로 즐겨찾기 관리
- 단계별 조리 방법 안내

### 사용자 인증
- 이메일 기반 회원가입/로그인
- 백업 코드를 통한 계정 복구
- 비밀번호 재설정 지원

---

## 아키텍처

### Clean Architecture

| 레이어 | 역할 | 구성 요소 |
|--------|------|-----------|
| **Presentation** | UI 표시 및 사용자 인터랙션 | ViewController, Custom View, Extension |
| **Domain** | 비즈니스 로직 및 엔티티 정의 | Ingredient, Recipe, UserInfo, CommonResponse |
| **Data** | 데이터 접근 및 변환 | DTO, Repository, Network Layer |

### Repository Pattern

| Repository | 역할 | 주요 메서드 |
|------------|------|-------------|
| **SignRepository** | 인증 관련 API | signIn, signUp, findPassword, modifyPassword, withdraw |
| **RecipeRepository** | 레시피 API | recommendRecipe, searchRecipe, bookMark, detailRecipe, savedRecipe |
| **IngredientRepository** | 식재료 API | closerIngredients, endIngredients, saveIngredient, modifyIngredient, deleteIngredient |
| **UserRepository** | 로컬 사용자 데이터 | getUserNickName, setUserNickName, deleteUserNickName |

### 프로젝트 구조

```
ReFree/
├── App/                          # 앱 진입점
│   ├── AppDelegate.swift
│   └── SceneDelegate.swift
│
├── Source/
│   ├── Common/                   # 공통 컴포넌트
│   │   ├── View/                 # AlertView, LoadingView, RFSearchBar
│   │   └── ViewController/       # RFModalViewController, HomeTabViewController
│   │
│   ├── Data/
│   │   ├── DTO/                  # API 요청/응답 객체
│   │   ├── Domain/               # 도메인 모델
│   │   └── Repository/           # Local/Remote 데이터 접근
│   │
│   ├── Home/                     # 유통기한 임박 알림
│   ├── Refrigerator/             # 식재료 목록
│   ├── RegisterIngredient/       # 식재료 등록
│   ├── Recipe/                   # 레시피 추천
│   ├── KindRecipe/               # 레시피 검색
│   ├── LogIn/                    # 로그인
│   ├── SignUp/                   # 회원가입
│   ├── Setting/                  # 설정
│   │
│   └── Util/
│       ├── Network/              # Network, NetworkError, Target Protocol
│       ├── Extension/            # UIView, UIColor, UIFont 등 17개 Extension
│       ├── KeyChain.swift        # 보안 토큰 저장
│       └── ValidationCheck.swift # 입력 검증
│
└── Resource/
    ├── Assets.xcassets/          # 이미지, 컬러
    └── Fonts/                    # Pretendard 폰트
```

---

## 기술 스택

| 카테고리 | 기술 |
|----------|------|
| **Language** | Swift 5.0+ |
| **UI Framework** | UIKit |
| **Layout** | SnapKit |
| **Reactive** | RxSwift, RxCocoa, RxGesture |
| **Networking** | Alamofire |
| **Image Loading** | Kingfisher |
| **Animation** | Lottie |
| **Builder Pattern** | Then |
| **Package Manager** | Swift Package Manager |

---

## 기술적 구현

### 1. 네트워크 레이어

Alamofire 기반 커스텀 HTTP 클라이언트를 구현하여 RxSwift Observable과 통합했습니다.

```swift
// Network.swift - 실제 구현
static func requestJSON<T: Decodable>(target: Target) -> Observable<T> {
    return Observable.create { emitter in
        guard var request = try? URLRequest(
            url: target.url,
            method: target.method,
            headers: target.header
        ) else {
            emitter.onError(NetworkError.makeRequestError)
            return Disposables.create()
        }

        request.httpBody = target.parameters

        let task = AF.request(request)
            .validate(statusCode: 200..<300)
            .responseDecodable(of: T.self) { response in
                switch response.result {
                case let .success(data):
                    emitter.onNext(data)
                case let .failure(error):
                    emitter.onError(error)
                }
            }

        return Disposables.create { task.cancel() }
    }
}
```

**헤더 기반 토큰 추출**

로그인/회원가입 시 응답 헤더에서 Authorization 토큰 또는 Certification 백업 코드를 자동 추출합니다.

```swift
// Network.swift - requestJSONHeader
if let token = response.response?.headers["Authorization"] {
    emitter.onNext((data, token))
} else if let backupCode = response.response?.headers["Certification"] {
    emitter.onNext((data, backupCode))
}
```

**이미지 업로드**

Multipart form-data로 이미지를 0.3 품질로 압축하여 업로드합니다.

```swift
// Network.swift - imageUpload
target.imageData.forEach { data in
    guard let imageData = data.image.jpegData(compressionQuality: 0.3)
    else { return }

    multipart.append(
        imageData,
        withName: data.withName,
        fileName: data.fileName,
        mimeType: data.mimeType
    )
}
```

---

### 2. 에러 핸들링

다층적 에러 처리 시스템을 구현했습니다.

| 레이어 | 에러 타입 | 처리 방식 |
|--------|-----------|-----------|
| **Network** | `NetworkError` | URLRequest 생성 실패, 토큰 에러 |
| **KeyChain** | `KeyChainError` | 인코딩/디코딩 실패, 토큰 미발견, OSStatus 에러 |
| **Response** | `CommonResponse` | 응답 코드별 분기 처리 (200, 401 등) |
| **Validation** | String Extension | 정규식 기반 이메일/비밀번호/인증코드 검증 |

```swift
// NetworkError.swift
enum NetworkError: Error {
    case makeRequestError  // URLRequest 생성 실패
    case tokenError        // 토큰이 정상적으로 발급되지 않음
}

// KeyChainError
enum KeyChainError: Error {
    case encodingFailed    // 토큰 인코딩 에러
    case decodingFailed    // 토큰 디코딩 에러
    case notFound          // 토큰을 찾을 수 없음
    case unhandledError(status: OSStatus)  // 예상치 못한 에러
}
```

**응답 코드 기반 처리**

```swift
// UIView+ResponseCheck.swift
func responseCheck(response: CommonResponse) -> Bool {
    switch response.code {
    case "200": return true
    case "401": loginExpired(); return false  // 로그인 만료 처리
    default:
        Alert.checkAlert(targetView: self, title: response.message, message: "")
        return false
    }
}
```

**입력값 검증**

```swift
// ValidationCheck.swift
extension String {
    func validateEmail() -> Bool {
        let emailRegEx1 = "[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{3}"
        let emailRegEx2 = "[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2}+\\.[A-Za-z]{2}"
        return NSPredicate(format: "SELF MATCHES %@", emailRegEx1).evaluate(with: self)
            || NSPredicate(format: "SELF MATCHES %@", emailRegEx2).evaluate(with: self)
    }

    func validatePassword() -> Bool {
        let passwordRegEx = "[A-Z0-9a-z._%+-]{8,}"  // 8자 이상
        return NSPredicate(format: "SELF MATCHES %@", passwordRegEx).evaluate(with: self)
    }

    func validateVerificationCode() -> Bool {
        let verificationCodeRegEx = "[A-Z0-9]{9}"  // 대문자+숫자 9자리
        return NSPredicate(format: "SELF MATCHES %@", verificationCodeRegEx).evaluate(with: self)
    }
}
```

---

### 3. Keychain 토큰 관리

iOS Keychain API를 활용하여 Access Token과 Refresh Token을 안전하게 저장합니다.

```swift
// KeyChain.swift
struct KeyChain {
    static let shared = KeyChain()

    enum TokenKind: String {
        case accessToken = "accessToken"
        case refreshToken = "refreshToken"
    }

    func addToken(kind: TokenKind, token: String) throws {
        guard let saveToken = token.data(using: .utf8) else {
            throw KeyChainError.encodingFailed
        }

        let query: [String: Any] = [
            kSecClass as String: kSecClassInternetPassword,
            kSecAttrType as String: kind.rawValue,
            kSecAttrServer as String: Network.server,
            kSecValueData as String: saveToken
        ]

        let status = SecItemAdd(query as CFDictionary, nil)
        guard status == errSecSuccess else {
            throw KeyChainError.unhandledError(status: status)
        }
    }

    func searchToken(kind: TokenKind) throws -> String {
        // SecItemCopyMatching으로 토큰 조회
    }

    func updateToken(kind: TokenKind, newToken: String) throws {
        // SecItemUpdate로 토큰 갱신
    }

    func deleteToken(kind: TokenKind) throws {
        // SecItemDelete로 토큰 삭제
    }
}
```

---

### 4. 애니메이션 구현

#### Lottie 로딩 애니메이션

```swift
// LoadingView.swift
final class LoadingView: UIView {
    private let loadingView = LottieAnimationView(name: "LoadingAnimation").then {
        $0.loopMode = .loop
        $0.play()
    }

    private let descriptionLabel = UILabel().then {
        $0.text = "OOO님을 위한\n레시피를 추천드릴게요!"
    }

    func setName(_ name: String) {
        descriptionLabel.text = "\(name)님을 위한\n레시피를 추천드릴게요!"
    }

    func play() { loadingView.play() }
    func stop() { loadingView.stop() }
}
```

#### 그라디언트 배경

6가지 그라디언트 타입을 지원하는 Extension을 구현했습니다.

```swift
// UIView+gradient.swift
extension UIView {
    enum BackgroundType {
        case mainConic       // 원형 그라디언트
        case mainAxial       // 상하 그라디언트 (흰색 → 배경색)
        case reverseMainAxial
        case blackAxial
        case halfBlackAxial  // 투명 → 검정
        case halfWhiteAxial  // 투명 → 흰색
    }

    func gradientBackground(type: BackgroundType) {
        switch type {
        case .mainAxial: mainAxialBackground()
        // ...
        }
    }

    private func setGradientLayer(
        type: CAGradientLayerType,
        colors: [CGColor],
        startPoint: CGPoint,
        endPoint: CGPoint,
        locations: [NSNumber]?
    ) {
        let gradientLayer = CAGradientLayer()
        gradientLayer.type = type
        gradientLayer.colors = colors
        gradientLayer.startPoint = startPoint
        gradientLayer.endPoint = endPoint
        gradientLayer.locations = locations
        gradientLayer.frame = self.bounds
        self.layer.addSublayer(gradientLayer)
    }
}
```

#### 캐러셀 UI

레시피 추천 화면에서 스케일 애니메이션이 적용된 수평 캐러셀을 구현했습니다.

```swift
// RecipeViewController.swift
private enum Const {
    static let itemSize = CGSize(
        width: Constant.screenSize.width * 0.7,
        height: Constant.screenSize.height * 0.45
    )
    static let itemSpacing = 30.0
    static var insetX: CGFloat {
        return (Constant.screenSize.width - itemSize.width) / 2.0
    }
}

// 스크롤 시 현재/이전 셀 스케일 애니메이션
func scrollViewDidScroll(_ scrollView: UIScrollView) {
    let scrolledOffset = scrollView.contentOffset.x + scrollView.contentInset.left
    let cellWidth = Const.itemSize.width + Const.itemSpacing
    let index = Int(round(scrolledOffset / cellWidth))

    guard previousIndex != index else { return }

    let prevCell = carouselCollectionView.cellForItem(at: IndexPath(row: previousIndex, section: 0))
    let currentCell = carouselCollectionView.cellForItem(at: IndexPath(row: index, section: 0))

    UIView.animate(withDuration: 0.5) {
        prevCell?.transform = CGAffineTransform(scaleX: 1, y: 1)
        currentCell?.transform = CGAffineTransform(scaleX: 1.1, y: 1.1)
    }

    self.previousIndex = index
}

// 페이징 스냅 구현
func scrollViewWillEndDragging(
    _ scrollView: UIScrollView,
    withVelocity velocity: CGPoint,
    targetContentOffset: UnsafeMutablePointer<CGPoint>
) {
    let scrolledOffsetX = targetContentOffset.pointee.x + scrollView.contentInset.left
    let cellWidth = Const.itemSize.width + Const.itemSpacing
    let index = round(scrolledOffsetX / cellWidth)
    targetContentOffset.pointee = CGPoint(
        x: index * cellWidth - scrollView.contentInset.left,
        y: scrollView.contentInset.top
    )
}
```

#### 사이드바 슬라이드 애니메이션

```swift
// RecipeViewController.swift
private func openSidebar() {
    sidebar.snp.remakeConstraints {
        $0.leading.equalToSuperview()
        $0.top.bottom.equalTo(view.safeAreaLayoutGuide)
        $0.width.equalTo(250)
    }

    UIView.animate(withDuration: 0.5) {
        self.view.layoutIfNeeded()
    }
}

private func closeSidebar() {
    sidebar.snp.remakeConstraints {
        $0.leading.equalToSuperview().offset(-280)
        // ...
    }

    UIView.animate(withDuration: 0.5) {
        self.view.layoutIfNeeded()
    }
}
```

#### 커스텀 Alert

RxSwift 기반의 커스텀 알림 뷰를 구현했습니다.

```swift
// AlertView.swift
final class AlertView: UIView {
    enum AlertType { case question, check }
    enum ButtonKind { case success, cancel }

    private let backgroundView = UIView().then {
        $0.layer.opacity = 0.7
        $0.backgroundColor = .black
    }

    func addAction(kind: ButtonKind, action: @escaping () -> ()) {
        switch kind {
        case .success:
            successButton.rx.tap.bind { _ in action() }.disposed(by: disposeBag)
        case .cancel:
            cancelButton.rx.tap.bind { _ in action() }.disposed(by: disposeBag)
        }
    }
}
```

---

### 5. RxSwift 데이터 바인딩

```swift
// RecipeViewController.swift - 레시피 추천 바인딩
private func bindRecommendRecipe() {
    recipeRepository.request(recommendRecipe: .recommendRecipe)
        .subscribe(
            onNext: { [weak self] (commonResponse, recipes) in
                guard let self, self.responseCheck(response: commonResponse)
                else { self?.loadingCompletion(); return }

                self.recipes = recipes
                self.carouselCollectionView.reloadData()
                self.loadingCompletion()
            },
            onError: { [weak self] error in
                guard let self else { return }
                Alert.errorAlert(viewController: self, errorMessage: error.localizedDescription)
                self.loadingCompletion()
            }
        )
        .disposed(by: disposeBag)
}

// 제스처 기반 사이드바 바인딩
let swipe = sidebar.rx.swipeGesture(.left).when(.recognized).map { _ in Void() }
let sidebarCloseButtonTap = sidebar.backButton.rx.tap.map { _ in Void() }

Observable.merge([swipe, sidebarCloseButtonTap])
    .subscribe { [weak self] _ in
        self?.closeSidebar()
    }
    .disposed(by: disposeBag)
```

---

## 화면 구성

| 홈 | 냉장고 | 식재료 등록 |
|:--:|:--:|:--:|
| 유통기한 임박 식재료 표시 | 보관 방법별 식재료 목록 | 카메라/갤러리 이미지 등록 |

| 레시피 | 레시피 검색 | 설정 |
|:--:|:--:|:--:|
| 맞춤 레시피 캐러셀 | 키워드 기반 검색 결과 | 계정 관리 |

---

## 설치 및 실행

### 요구 사항

- Xcode 14.0+
- iOS 15.0+
- Swift 5.0+

### 환경 설정

`Info.plist`에서 다음 값들을 설정해야 합니다:

| Key | 설명 |
|-----|------|
| `REFREE_SERVER_DOMAIN` | 백엔드 API 서버 URL |
| `REFREE_SERVICE_POLICY` | 서비스 이용약관 URL |
| `REFREE_PRIVACY_POLICY` | 개인정보처리방침 URL |

---

## 권한 요청

| 권한 | 용도 |
|------|------|
| **카메라** | 식재료 사진 촬영 |
| **사진 라이브러리** | 인증 코드 이미지 저장, 갤러리에서 식재료 이미지 선택 |
