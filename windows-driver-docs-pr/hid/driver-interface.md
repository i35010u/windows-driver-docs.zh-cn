---
title: 驱动程序接口
description: 驱动程序接口
ms.assetid: cb5e06c3-6add-4eba-b794-861d567a3047
keywords:
- 强制反馈驱动程序 WDK HID，支持方法
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e13c09772a151d3f0b04d670b10382e573acbfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575551"
---
# <a name="driver-interface"></a>驱动程序接口





如果强制反馈驱动程序是基于 COM 的由 DirectInput 创建驱动程序的实例。 如果该接口指定为"VJoyD"，则由 VJoyD 加载 VJoyD 微型驱动程序。 这两个驱动程序路径支持以下导出的方法：

[*DestroyEffect*](https://msdn.microsoft.com/library/windows/hardware/ff538410)

[*初始化*](https://msdn.microsoft.com/library/windows/hardware/ff541025)

[*DownloadEffect*](https://msdn.microsoft.com/library/windows/hardware/ff538601)

[*GetEffectStatus*](https://msdn.microsoft.com/library/windows/hardware/ff538772)

[*GetForceFeedbackState*](https://msdn.microsoft.com/library/windows/hardware/ff538776)

[*Escape*](https://msdn.microsoft.com/library/windows/hardware/ff538680)

[*SendForceFeedbackCommand*](https://msdn.microsoft.com/library/windows/hardware/ff543387)

[*SetGain*](https://msdn.microsoft.com/library/windows/hardware/ff543406)

[*StartEffect*](https://msdn.microsoft.com/library/windows/hardware/ff543458)

[*StopEffect*](https://msdn.microsoft.com/library/windows/hardware/ff543460)

由所有强制反馈设备支持此功能。

 

 




