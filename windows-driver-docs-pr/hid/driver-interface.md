---
title: 驱动程序接口
description: 驱动程序接口
ms.assetid: cb5e06c3-6add-4eba-b794-861d567a3047
keywords:
- 强制反馈驱动程序 WDK HID，支持方法
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c2eda901ce83fdfdfa282f9d9f305592142ce323
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375742"
---
# <a name="driver-interface"></a>驱动程序接口





如果强制反馈驱动程序是基于 COM 的由 DirectInput 创建驱动程序的实例。 如果该接口指定为"VJoyD"，则由 VJoyD 加载 VJoyD 微型驱动程序。 这两个驱动程序路径支持以下导出的方法：

[*DestroyEffect*](https://docs.microsoft.com/previous-versions/ff538410(v=vs.85))

[*初始化*](https://docs.microsoft.com/previous-versions/ff541025(v=vs.85))

[*DownloadEffect*](https://docs.microsoft.com/previous-versions/ff538601(v=vs.85))

[*GetEffectStatus*](https://docs.microsoft.com/previous-versions/ff538772(v=vs.85))

[*GetForceFeedbackState*](https://docs.microsoft.com/previous-versions/ff538776(v=vs.85))

[*Escape*](https://docs.microsoft.com/previous-versions/ff538680(v=vs.85))

[*SendForceFeedbackCommand*](https://docs.microsoft.com/previous-versions/ff543387(v=vs.85))

[*SetGain*](https://docs.microsoft.com/previous-versions/ff543406(v=vs.85))

[*StartEffect*](https://docs.microsoft.com/previous-versions/ff543458(v=vs.85))

[*StopEffect*](https://docs.microsoft.com/previous-versions/ff543460(v=vs.85))

由所有强制反馈设备支持此功能。

 

 




