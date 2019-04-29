---
title: 测试系统方案
author: windows-driver-content
description: 此测试侧重于确保环境光线传感器 (ALS) 正常工作后系统电源事件，例如睡眠或休眠状态。
ms.assetid: f2778853-ddc8-4118-aa58-9df6dab53b7a
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: de2faa4012f6c103ce4a36b64c7b9c35f69d3995
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391554"
---
# <a name="testing-system-scenarios"></a>测试系统方案

此测试侧重于确保环境光线传感器 (ALS) 正常工作后系统电源事件，例如睡眠或休眠状态。

## <a name="set-up"></a>设置

通读[测试要求](testing-MALT-building-a-light-testing-tool.md)一部分，以确保已满足测试的要求。

## <a name="brightness-stress-test-procedures"></a>亮度压力测试过程

1. 在 SUT 上运行`MALTUtil.exe /stress`。
2. 请等待。 此测试将需要大约 15 分钟。 测试将放置在系统进入睡眠状态的同时调整光的亮度。  测试将寻找它需要的系统浅色和如果传感器生成超出范围的值在初始化过程中的更改做出反应时间。
3. 在测试完成后，结果将显示在屏幕上。

请参阅[本白皮书](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update)有关 Microsoft 的完整指导集成光线传感器和环境光线响应曲线。
