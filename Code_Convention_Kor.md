# 🎯 DX12 + C++ 게임 개발 코딩 컨벤션

최종 수정일: 2025.06.08 | 프로젝트: DX12 게임 엔진

---

## 📁 1. 프로젝트 구조 (DevRniman)

### 전체 솔루션 구조
```
DevRniman/
├── DevRniman.sln                    // 메인 솔루션 파일
├── Engine/                          // 엔진 코어 모듈들
│   ├── Core/                        // 기본 시스템, 메모리 관리
│   │   ├── Core.vcxproj
│   │   ├── src/
│   │   └── include/Core/
│   ├── Graphics/                    // DirectX 12 렌더링 코어
│   │   ├── Graphics.vcxproj
│   │   ├── src/DX12/
│   │   └── include/Graphics/DX12/
│   └── Math/                        // 수학 라이브러리
│       ├── Math.vcxproj
│       ├── src/
│       └── include/Math/
├── Platform/                        // 플랫폼 추상화 및 Windows 구현
│   ├── Platform.vcxproj
│   └── src/
│       ├── Common/                  // 플랫폼 공통 인터페이스
│       ├── Windows/                 // Windows 특화 구현
│       └── Application/             // 애플리케이션 프레임워크
├── Samples/                         // 샘플 프로젝트들
│   ├── HelloTriangle/
│   ├── BasicLighting/
│   └── TextureMapping/
├── Tools/                           // 개발 도구들
│   ├── ShaderCompiler/
│   ├── AssetConverter/
│   └── ResourcePacker/
├── Assets/                          // 공통 리소스
│   ├── Shaders/
│   ├── Textures/
│   ├── Models/
│   └── Materials/
├── bin/                             // 빌드 출력 디렉토리
├── intermediate/                    // 중간 빌드 파일
└── external/                        // 외부 라이브러리
```

### 빌드 설정
- **프로젝트 타입**: Engine/Platform → Static Library (.lib), Samples/Tools → Application (.exe)
- **출력 디렉토리**: `$(SolutionDir)bin\$(Configuration)\`
- **중간 파일**: `$(SolutionDir)intermediate\$(ProjectName)\$(Configuration)\`
- **의존성**: Samples → Platform → Engine

---

## 🏷️ 2. 네이밍 규칙 & 네임스페이스

### 네임스페이스 구조
```cpp
namespace rniman
{
    namespace core          // Core 프로젝트
    {
        class Logger;
        class Assert;
    }
    
    namespace graphics      // Graphics 프로젝트
    {
        namespace dx12      // DirectX 12 특화
        {
            class Device;
            class CommandQueue;
            class Buffer;
        }
        
        class RenderTarget;
        class Material;
    }
    
    namespace math          // Math 프로젝트
    {
        class Vector3;
        class Matrix4;
    }
    
    namespace platform      // Platform 프로젝트
    {
        namespace windows   // Windows 특화
        {
            class WindowsWindow;
            class WindowsInput;
        }
        
        class IWindow;      // 인터페이스
        class IInput;
        class Application;
    }
}
```

### 클래스 & 구조체
```cpp
class RenderDevice;           // PascalCase
struct WindowInfo;            // PascalCase
enum class ResourceState;     // PascalCase
```

### 함수
```cpp
void Initialize();            // PascalCase, 동사로 시작
bool IsValidDevice();         // bool 반환 시 Is/Has/Can/Should 접두어
void CreateRenderTarget();    // 명확한 동사 사용
```

### 변수
```cpp
// 지역 변수
int frameIndex = 0;           // camelCase

// 멤버 변수
class Renderer {
private:
    UINT mFrameIndex{0};      // m + PascalCase
    static int sInstanceCount; // s + PascalCase (정적)
};

// 전역 변수
Renderer* gRenderer = nullptr; // g + PascalCase

// 구조체 멤버
struct Vertex {
    float x, y, z;            // camelCase, 접두어 없음
};
```

---

## ⚙️ 3. 코드 스타일

### 기본 규칙
```cpp
// ✅ 중괄호 항상 사용 - BSD(Allman) 스타일
if (condition) 
{
    DoSomething();
}

// ✅ 포인터는 타입과 붙임
ID3D12Device* device = nullptr;

// ✅ nullptr 사용, NULL 금지
ComPtr<ID3D12Device> mDevice = nullptr;

// ✅ auto는 타입이 명확할 때만
auto result = device->CreateCommandQueue(&desc, IID_PPV_ARGS(&queue));
```

### 변수 초기화
```cpp
// 지역 변수 - = 대입 초기화 기본
int count = 0;
float fov = 60.0f;
std::vector<int> list = {1, 2, 3};    // 컨테이너는 {} 허용

// 멤버 변수 - {} 중괄호 초기화 허용
class Renderer {
private:
    UINT mFrameIndex{0};
    ComPtr<ID3D12Device> mDevice{};
};

// 전역/정적 상수
constexpr int MAX_FRAME_COUNT{3};
```

### 복합 객체 초기화
```cpp
// 여러 항목 시 줄바꿈 + 정렬
std::array<CD3DX12_DESCRIPTOR_RANGE, 3> ranges = {
    CD3DX12_DESCRIPTOR_RANGE(D3D12_DESCRIPTOR_RANGE_TYPE_CBV, 1, 0),      // b0
    CD3DX12_DESCRIPTOR_RANGE(D3D12_DESCRIPTOR_RANGE_TYPE_SRV, 2, 0),      // t0~t1
    CD3DX12_DESCRIPTOR_RANGE(D3D12_DESCRIPTOR_RANGE_TYPE_SAMPLER, 1, 0),  // s0
};
```

---

## 💾 4. 메모리 관리

### 스마트 포인터 우선 사용
```cpp
// DirectX COM 객체
using Microsoft::WRL::ComPtr;
ComPtr<ID3D12Device> mDevice;

// 일반 객체
std::unique_ptr<RenderTarget> mRenderTarget;    // 단독 소유
std::shared_ptr<Texture> mTexture;              // 공유 필요 시
```

### 함수 매개변수 전달
```cpp
// 읽기 전용 - const 참조
void ProcessTexture(const Texture& texture);
void UpdateBuffer(const std::shared_ptr<Buffer>& buffer);

// 포인터는 null 가능성이 있을 때만
void SetOptionalTexture(Texture* texture = nullptr);
```

---

## 🔒 5. 상수 정의

```cpp
// ✅ constexpr 사용 (컴파일 타임)
constexpr int MAX_FRAME_COUNT = 3;
constexpr float PI = 3.14159f;

// ✅ 전역 constexpr는 ALL_CAPS
constexpr UINT SWAP_CHAIN_BUFFER_COUNT = 2;

// ✅ 런타임 상수는 const
const std::string CONFIG_FILE_PATH = GetConfigPath();

// ❌ #define 금지 (외부 API 제외)
// #define MAX_COUNT 100  // 사용 금지
```

---

## 🔐 6. 접근 제어

### const 사용 원칙
```cpp
class RenderDevice {
public:
    // 읽기 전용 매개변수
    void SetViewport(const D3D12_VIEWPORT& viewport);
    
    // 읽기 전용 멤버 함수
    UINT GetFrameIndex() const;
    ID3D12Device* GetDevice() const { return mDevice.Get(); }

private:
    ComPtr<ID3D12Device> mDevice;
    UINT mFrameIndex{0};
};
```

### 캡슐화 원칙
```cpp
class Renderer {
public:
    // 외부 인터페이스
    void Initialize();
    void Render();
    
    // 접근자/설정자
    void SetFrameIndex(UINT index);
    UINT GetFrameIndex() const;

private:
    // 내부 구현 함수
    void CreateCommandObjects();
    void InitializeRenderTargets();
    
    // 멤버 변수 (항상 private)
    UINT mFrameIndex{0};
    ComPtr<ID3D12Device> mDevice;
};
```

---

## 📦 7. 네임스페이스 & 헤더

### 네임스페이스 사용
```cpp
// 허용되는 using 선언
using namespace std;
using Microsoft::WRL::ComPtr;

// 프로젝트 네임스페이스 별칭
namespace rni = rniman;
namespace gfx = rniman::graphics;
namespace dx12 = rniman::graphics::dx12;
```

### 헤더 include 최적화
```cpp
// Graphics/DX12/D3D12Device.h
#pragma once

// 전방 선언 우선 사용
namespace rniman::graphics::dx12 
{
    class CommandQueue;
    class Buffer;
}

// 필요한 경우에만 include
#include <d3d12.h>
#include <wrl/client.h>

namespace rniman::graphics::dx12 
{
    class Device 
    {
        // 전방 선언된 타입의 포인터/참조 사용
        void Initialize(const CommandQueue& queue);
        void CreateBuffer(Buffer* buffer);
    };
}
```

```cpp
// Graphics/DX12/D3D12Device.cpp
#include "Graphics/DX12/D3D12Device.h"

// cpp에서 실제 헤더 include
#include "Graphics/DX12/D3D12CommandQueue.h"
#include "Graphics/DX12/D3D12Buffer.h"
```

---

## 🏗️ 8. 클래스 구성

### 접근 지정자 순서 & 멤버 정렬
```cpp
namespace rniman::graphics::dx12 
{
    class Device 
    {
    public:
        // 1. 생성자/소멸자
        Device();
        ~Device();
        
        // 2. 정적 생성 함수
        static std::shared_ptr<Device> Create();
        
        // 3. 주요 API 함수 (기능 흐름 순)
        void Initialize();
        void CreateCommandQueue();
        void CreateBuffer();
        void Shutdown();
        
        // 4. Getter/Setter
        ID3D12Device* GetDevice() const;
        void SetDebugMode(bool enabled);

    protected:
        // 파생 클래스용 protected 함수
        virtual void OnInitialize();

    private:
        // 내부 유틸 함수
        void CreateInternalResources();
        void ResetState();
        
        // 멤버 변수 (항상 마지막)
        Microsoft::WRL::ComPtr<ID3D12Device> mDevice;
        UINT mFrameIndex{0};
        bool mInitialized{false};
    };
}
```

---

## 📝 9. 함수 정의 스타일

### 매개변수 줄바꿈 (4개 이상 권장)
```cpp
// 함수 선언
void CreateRenderPipeline(
    ID3D12Device* device,
    const std::wstring& shaderPath,
    const D3D12_INPUT_LAYOUT_DESC& inputLayout,
    DXGI_FORMAT renderTargetFormat
);

// 함수 호출
auto barrier = CD3DX12_RESOURCE_BARRIER::Transition(
    backBuffer.Get(),
    D3D12_RESOURCE_STATE_RENDER_TARGET,  // before
    D3D12_RESOURCE_STATE_PRESENT         // after
);
```

---

## 🏛️ 10. 의존성 관리

### 계층별 전역 접근 허용 범위 (ex.싱글톤)

| 계층 | 전역 접근 | 설명 |
|------|----------|------|
| **Engine/App Layer** | ✅ 허용 | 애플리케이션 초기화 계층 |
| **Manager Layer** | ⚠️ 제한적 허용 | 명시적 전달 우선, 전역 접근은 임시 수단 |
| **Component/Object Layer** | ❌ 지양 | 의존 객체를 파라미터로 전달 |
| **Utility/Math Layer** | 🚫 절대 금지 | 완전한 독립성 유지 |

### 의존성 주입 예시
```cpp
// ❌ Component가 직접 싱글톤 접근
namespace rniman::graphics 
{
    class MeshRenderer 
    {
        void Render() 
        {
            Engine::GetInstance().GetRenderer().Draw();  // 지양
        }
    };
}

// ✅ 명시적 의존성 전달
namespace rniman::graphics 
{
    class MeshRenderer 
    {
        void Render(dx12::Device& device, dx12::CommandQueue& cmdQueue) 
        {
            device.CreateBuffer();
            cmdQueue.ExecuteCommandLists();  // 권장
        }
    };
}
```

---

## 📊 11. 매개변수 전달 가이드

### shared_ptr 전달 방식
```cpp
// 읽기 전용 참조 (기본 권장)
void ProcessTexture(const std::shared_ptr<rniman::graphics::Texture>& texture);

// 공유 및 내부 저장
void SetTexture(std::shared_ptr<rniman::graphics::Texture> texture);

// 소유권 이동
void TakeOwnership(std::shared_ptr<rniman::graphics::Texture>&& texture);

// 호출자 포인터 변경
void ReplaceTexture(std::shared_ptr<rniman::graphics::Texture>& texture);
```

---

## ✅ 12. 권장 사항

### 컨테이너 사용
```cpp
// ✅ STL 컨테이너 사용
std::array<float, 16> matrix;        // 정적 크기
std::vector<Vertex> vertices;        // 가변 크기

// ❌ C 스타일 배열 지양
float matrix[16];                    // 지양
```

### 열거형 정의
```cpp
// ✅ enum class 사용
enum class ResourceState {
    Common,
    RenderTarget,
    CopyDest
};

// ❌ 상수 정의용 enum 금지
// enum { MAX_COUNT = 100 };  // 대신 constexpr 사용
```

---

## 🚫 13. 금지 사항

- `#define`을 통한 상수 정의 (외부 API 제외)
- `NULL` 사용 (`nullptr` 사용)
- C 스타일 배열 (STL 컨테이너 사용)
- 전역 접근 매크로 (`DEVICE`, `COMMAND_LIST` 등)
- 과도한 전역 싱글톤 의존성

---

## 📋 코드 리뷰 체크리스트

- [ ] 네이밍 규칙 준수 (PascalCase, camelCase, 접두어)
- [ ] 스마트 포인터 적절히 사용
- [ ] const 정확성 확인
- [ ] 전방 선언 활용으로 컴파일 시간 최적화
- [ ] 접근 지정자 올바른 사용 (최소 권한 원칙)
- [ ] 의존성 명시적 전달
- [ ] 매개변수 4개 이상 시 줄바꿈
- [ ] constexpr/const 적절히 사용

---

*이 컨벤션은 DX12 게임 엔진 프로젝트의 코드 품질과 유지보수성을 향상시키기 위한 가이드라인입니다.*