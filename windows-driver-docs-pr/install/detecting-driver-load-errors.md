---
title: 检测驱动程序加载错误
description: 检测驱动程序加载错误
ms.assetid: 1233aa87-067e-4f58-add5-3737f8ddd358
keywords:
- 驱动程序负载错误 WDK 驱动程序签名
- 错误 WDK 驱动程序签名
- 检测驱动程序加载
- 加载错误 WDK 驱动程序签名
- 状态信息 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 192340bf06399775b83d66b6b15fdb0635326472
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346193"
---
# <a name="detecting-driver-load-errors"></a>检测驱动程序加载错误


若要检测是否加载的驱动程序，请检查设备在设备管理器的状态。 如果[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)阻止驱动程序加载，因为未正确签名的驱动程序，从设备状态消息会指示 Windows 无法加载该驱动程序和驱动程序可能已损坏或缺少。 如果发生这种情况，则可以使用[代码完整性诊断系统日志事件](code-integrity-diagnostic-system-log-events.md)来进一步诊断问题。

以下屏幕截图显示设备的状态消息，指示 Windows 无法加载设备驱动程序和驱动程序可能已损坏或缺少的类型。

![未签名驱动程序错误消息的屏幕截图](images/signing-driver-load-error-message.png)

 

 





