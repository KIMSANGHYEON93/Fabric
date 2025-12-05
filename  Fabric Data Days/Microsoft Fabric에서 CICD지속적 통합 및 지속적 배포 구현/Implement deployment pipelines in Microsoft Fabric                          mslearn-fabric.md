---
title: "Implement deployment pipelines in Microsoft Fabric |                         mslearn-fabric"
source: "https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/21-implement-cicd.html"
author:
published:
created: 2025-12-03
description:
tags:
  - "clippings"
---
## Microsoft Fabric에서 배포 파이프라인 구현

Microsoft Fabric의 배포 파이프라인을 사용하면 개발, 테스트, 프로덕션 환경 등 여러 환경 간에 Fabric 항목의 콘텐츠에 적용된 변경 사항을 복사하는 프로세스를 자동화할 수 있습니다. 배포 파이프라인을 사용하면 최종 사용자에게 도달하기 전에 콘텐츠를 개발하고 테스트할 수 있습니다. 이 연습에서는 배포 파이프라인을 만들고 파이프라인에 단계를 할당합니다. 그런 다음 개발 작업 영역에서 콘텐츠를 만들고 배포 파이프라인을 사용하여 개발, 테스트, 프로덕션 파이프라인 단계 간에 콘텐츠를 배포합니다.

> **참고**: 이 연습을 완료하려면 Fabric 작업 영역 관리자 역할의 구성원이어야 합니다. 역할을 할당하려면 [Microsoft Fabric 작업 영역의 역할을](https://learn.microsoft.com/en-us/fabric/get-started/roles-workspaces) 참조하세요.

이 실험을 완료하는 데 약 **20** 분이 걸립니다.

## 작업 공간 만들기

Fabric 평가판을 활성화하여 세 개의 작업 공간을 만듭니다.

1. 브라우저 에서 [Microsoft Fabric 홈페이지](https://app.fabric.microsoft.com/home?experience=fabric) 로 이동하여 `https://app.fabric.microsoft.com/home?experience=fabric` Fabric 자격 증명을 사용하여 로그인합니다.
2. 왼쪽 메뉴 모음에서 **작업 공간을** 선택하세요 (아이콘은 🗇와 비슷합니다).
3. *개발이라는 이름의 새 작업 공간을 만들고 Fabric 용량( 평가판*, *프리미엄* 또는 *Fabric* ) 을 포함하는 라이선스 모드를 선택합니다 .
4. 1단계와 2단계를 반복하여 Test와 Production이라는 이름의 작업 공간을 두 개 더 만듭니다. 작업 공간은 Development, Test, Production입니다.
5. 왼쪽 메뉴 막대에서 **작업 공간** 아이콘을 선택하고 개발, 테스트, 프로덕션이라는 이름의 세 개의 작업 공간이 있는지 확인하세요.

> **참고**: 작업 공간에 고유한 이름을 입력하라는 메시지가 표시되면 개발, 테스트 또는 프로덕션이라는 단어 뒤에 하나 이상의 난수를 추가합니다.

## 배포 파이프라인 만들기

다음으로, 배포 파이프라인을 만듭니다.

1. 왼쪽 메뉴 모음에서 **작업 공간을** 선택합니다.
2. **배포 파이프라인을** 선택한 다음 **새 파이프라인을** 선택합니다.
3. **새 배포 파이프라인 추가** 창 에서 파이프라인에 고유한 이름을 지정하고 **다음을** 선택합니다.
4. 새 파이프라인 창에서 **만들기 및 계속을** 선택합니다.

## 배포 파이프라인 단계에 작업 공간 할당

배포 파이프라인의 각 단계에 작업 공간을 할당합니다.

1. 왼쪽 메뉴 표시줄에서 생성한 파이프라인을 선택합니다.
2. 나타나는 창에서 각 배포 단계에서 **작업 공간 할당** 아래의 옵션을 확장하고 단계 이름과 일치하는 작업 공간 이름을 선택합니다.
3. 각 배포 단계에 대해 '할당' 체크 **표시를 선택합니다.**

[![Screenshot of deployment pipeline.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/deployment-pipeline.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/deployment-pipeline.png)

## 콘텐츠 만들기

Fabric items haven’t been created in your workspaces yet. Next, create a lakehouse in the development workspace.

1. In the menu bar on the left, select **Workspaces**.
2. Select the **Development** workspace.
3. Select **New Item**.
4. In the window that appears, select **Lakehouse** and in the **New lakehouse window**, name the lakehouse, **LabLakehouse**. Make sure the “Lakehouse schemas (Public Preview)” option is disabled.
5. Select **Create**.
6. In the Lakehouse Explorer window, select **Start with sample data** to populate the new lakehouse with data.

[![Screenshot of Lakehouse Explorer.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/lakehouse-explorer.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/lakehouse-explorer.png)

1. Select the sample **NYCTaxi**.
2. In the menu bar on the left, select the pipeline you created.
3. Select the **Development** stage, and under the deployment pipeline canvas you can see the lakehouse you created as a stage item. In the left edge of the **Test** stage, there’s an **X** within a circle. The **X** indicates that the Development and Test stages aren’t synchronized.
4. Select the **Test** stage and under the deployment pipeline canvas you can see that the lakehouse you created is only a stage item in the source, which in this case refers to the **Development** stage.

[![Screenshot the deployment pipeline showing content mismatches between stages.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/lab-pipeline-compare.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/lab-pipeline-compare.png)

## Deploy content between stages

Deploy the lakehouse from the **Development** stage to the **Test** and **Production** stages.

1. Select the **Test** stage in the deployment pipeline canvas.
2. Under the deployment pipeline canvas, select the checkbox next to the Lakehouse item. Then select the **Deploy** button to copy the lakehouse in its current state to the **Test** stage.
3. In the **Deploy to next stage** window that appears, select **Deploy**. There is now an X in a circle in the Production stage in the deployment pipeline canvas. The lakehouse exists in the Development and Test stages but not yet in the Production stage.
4. Select the **Production** stage in the deployment canvas.
5. Under the deployment pipeline canvas, select the checkbox next to the Lakehouse item. Then select the **Deploy** button to copy the lakehouse in its current state to the **Production** stage.
6. In the **Deploy to next stage** window that appears, select **Deploy**. The green check marks between the stages indicates that all stages in sync and contain the same content.
7. Using deployment pipelines to deploy between stages also updates the content in the workspaces corresponding to the deployment stage. Let’s confirm.
8. In the menu bar on the left, select **Workspaces**.
9. Select the **Test** workspace. The lakehouse was copied there.
10. Open the **Production** workspace from the **Workspaces** icon on the left menu. The lakehouse was copied to the Production workspace too.

## Clean up

In this exercise, you created a deployment pipeline, and assigned stages to the pipeline. Then you created content in a development workspace and deployed it between pipeline stages using deployment pipelines.

- In the left navigation bar, select **Deployment pipelines**, select your pipeline, and then select **Delete this pipeline** from the settings menu to remove the deployment pipeline.

[![Screenshot of deployment pipeline, highlighting the Delete pipeline action.](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/delete-pipeline.png)](https://microsoftlearning.github.io/mslearn-fabric/Instructions/Labs/Images/delete-pipeline.png)

- After deleting the pipeline, select the icon for each workspace to view all of the items it contains.
- In the menu on the top toolbar, select **Workspace settings**.
- In the **General** section, select **Remove this workspace**.