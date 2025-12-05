---
title: "Implement deployment pipelines - Training"
source: "https://learn.microsoft.com/en-us/training/modules/implement-cicd-in-fabric/4-implement-deployment-pipelines"
author:
  - "[[wwlpublish]]"
published:
created: 2025-12-03
description: "Learn how to implement deployment pipelines in Microsoft Fabric."
tags:
  - "clippings"
---
## 배포 파이프라인 구현

100 경험치

파이프라인은 콘텐츠의 업데이트, 테스트 및 정기적인 업데이트를 보장하는 지속적 통합/지속적 배포(CI/CD) 방식을 지원합니다. 파이프라인은 콘텐츠 개발 수명 주기의 개발, 테스트 및 프로덕션 단계를 통해 콘텐츠의 이동을 자동화하는 방법입니다.

## 배포 파이프라인이란 무엇인가요?

Fabric 배포 파이프라인은 개발, 테스트, 운영 등 다양한 환경에 Fabric 항목을 배포하는 데 도움이 됩니다. 최종 사용자에게 도달하기 전에 Fabric에서 콘텐츠를 개발하고 테스트할 수 있습니다.

## 배포 파이프라인 만들기

배포 파이프라인은 두 가지 방법을 사용하여 만들 수 있습니다.

- Fabric의 왼쪽 탐색 창에 있는 **작업 공간** 아이콘을 사용합니다.
- 작업 공간 상단의 **배포 파이프라인 만들기** 아이콘 사용

배포 파이프라인을 생성하려면 다음 단계를 따르세요.

1. 왼쪽 탐색 창에서 **작업 공간** 아이콘을 선택한 다음 **배포 파이프라인을 선택합니다.**
2. **새 파이프라인을** 선택하세요 . 파이프라인 이름을 지정하고 **다음을** 선택하세요.
3. 파이프라인의 단계를 정의하고 이름을 지정하세요. 그런 다음 **'만들기 및 계속'을 선택하세요.**
	![파이프라인 단계 선택기의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl-data-ai/implement-cicd-in-fabric/media/create-stages.png)
	파이프라인 단계 선택기의 스크린샷입니다.
4. 스테이지에 작업 공간을 할당하세요. 그런 다음 스테이지 옆의 녹색 확인 표시를 선택하세요. 이제 파이프라인에 콘텐츠를 배포할 준비가 되었습니다.
	![작업 공간 할당 인터페이스의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl-data-ai/implement-cicd-in-fabric/media/assign-workspace.png)
	작업 공간 할당 인터페이스의 스크린샷입니다.

## 파이프라인 단계에 콘텐츠 배포

배포 프로세스를 통해 파이프라인의 한 단계에서 다른 단계로, 일반적으로 개발 단계에서 테스트 단계로, 테스트 단계에서 프로덕션 단계로 콘텐츠를 복제할 수 있습니다.

스테이지 간에 콘텐츠를 배포하려면 배포할 스테이지를 선택한 다음, "배포 위치" 드롭다운 상자에서 스테이지를 선택하고 "배포" 버튼을 클릭합니다 **.** **배포** 프로세스는 모든 작업 공간 콘텐츠를 대상 스테이지에 복사합니다. 다음 이미지에는 개발 스테이지에만 존재하는 데이터 파이프라인이 있는데, 개발 스테이지에서 **"배포"를** 선택하면 이 파이프라인이 테스트 스테이지로 이동합니다.

![콘텐츠 배포 인터페이스의 스크린샷.](https://learn.microsoft.com/en-us/training/wwl-data-ai/implement-cicd-in-fabric/media/deploy-content.png)

콘텐츠 배포 인터페이스의 스크린샷.

## Git을 사용하여 배포 파이프라인 사용

배포 파이프라인은 Git 브랜치와 함께 사용할 수 있습니다. 이는 각 환경의 콘텐츠가 서로 다른 Git 저장소 또는 브랜치에 있는 경우 개발, 테스트 및 프로덕션 환경 간에 콘텐츠를 홍보하는 데 사용됩니다.

Git 브랜치와 함께 배포 파이프라인을 사용하려면:

1. 이 페이지의 "배포 파이프라인 만들기" 섹션에 있는 지침에 따라 배포 파이프라인을 만들고 각 단계를 작업 공간에 할당하세요.
2. 배포 파이프라인의 각 작업 공간을 **작업 공간 설정** 의 **Git 통합** 에서 Git 저장소와 브랜치에 할당합니다.
	![작업 공간과 Git 공급자 연결 인터페이스의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl-data-ai/implement-cicd-in-fabric/media/connect-git.png)
	작업 공간과 Git 공급자 연결 인터페이스의 스크린샷입니다.
3. **이 페이지의 "파이프라인 스테이지에 콘텐츠 배포"** 섹션에 설명된 대로 파이프라인의 배포 버튼을 사용하여 스테이징 환경 간에 콘텐츠를 배포하세요 . 이렇게 하면 Fabric 환경 간에 콘텐츠가 이동하지만, *작업 공간에서 수동으로 업데이트하기 전까지는 Git 저장소가 업데이트되지 않습니다.*
	아래 이미지에서 배포 단계 상자의 체크 표시는 *Fabric의* 배포 파이프라인의 세 가지 스테이징 환경 모두에 데이터 파이프라인 항목이 존재하고 Fabric 단계가 동기화되었음을 나타냅니다.
	![파일이 Git과 동기화되기 전 파이프라인의 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl-data-ai/implement-cicd-in-fabric/media/pipeline-presync.png)
	파일이 Git과 동기화되기 전 파이프라인의 스크린샷입니다.
	배포 파이프라인의 일부인 테스트 또는 프로덕션 작업 공간에서 **소스 제어를** 선택하면 파이프라인이 Git 저장소와 동기화되지 않은 것을 확인할 수 있습니다.
	![커밋되지 않은 항목을 보여주는 작업 공간의 스크린샷과 파일이 아직 Git과 동기화되지 않은 소스 제어 상자를 보여주는 스크린샷입니다.](https://learn.microsoft.com/en-us/training/wwl-data-ai/implement-cicd-in-fabric/media/git-not-updated.png)
	커밋되지 않은 항목을 보여주는 작업 공간의 스크린샷과 파일이 아직 Git과 동기화되지 않은 소스 제어 상자를 보여주는 스크린샷입니다.
4. 테스트 작업 공간과 저장소를 동기화하려면 이전 이미지에 표시된 **소스 제어** 창 에서 **커밋 버튼을 선택합니다.**