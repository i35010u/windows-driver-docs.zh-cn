---
title: 测试系统方案
description: 此测试重点在于确保环境光线传感器 (ALS) 在发生系统电源事件（如睡眠或休眠）后正常工作。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 553feb8f89fb7089fb214296d6b98e79e17efc58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805073"
---
# <a name="testing-system-scenarios"></a>测试系统方案

此测试重点在于确保环境光线传感器 (ALS) 在发生系统电源事件（如睡眠或休眠）后正常工作。

## <a name="set-up"></a>设置

通读 [测试要求](testing-MALT-building-a-light-testing-tool.md) 部分，以确保满足测试的要求。

## <a name="brightness-stress-test-procedures"></a>亮度压力测试过程

1. 在 SUT 上，运行 `MALTUtil.exe /stress` 。
2. 再. 此测试需要大约15分钟。 测试将调整光源的亮度，同时使系统进入睡眠状态。  该测试将寻找系统响应光线变化所需的时间，以及在初始化期间传感器是否生成范围外的值。
3. 测试完成后，结果将显示在屏幕上。

请参阅 [此白皮书](/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) ，了解有关如何集成光源传感器和环境光线响应曲线的 Microsoft 完整指导。
