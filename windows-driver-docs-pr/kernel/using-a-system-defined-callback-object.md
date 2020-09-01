---
title: 使用系统定义的回调对象
description: 使用系统定义的回调对象
ms.assetid: 1f1a2fc1-e698-41f7-84e4-9db091def690
keywords:
- 回叫对象 WDK 内核
- 系统定义的回叫对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aafec630175b1ae85c0f7b335949470503bf182
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187727"
---
# <a name="using-a-system-defined-callback-object"></a>使用系统定义的回调对象





系统为驱动程序使用定义了三个回调对象：

**\\回调 \\ SetSystemTime**

**\\回调 \\ PowerState**

**\\回调 \\ ProcessorAdd**

使用系统时间 (的驱动程序例如，文件系统驱动程序) 可能注册** \\ 回调 \\ SetSystemTime**回调对象。 当系统时间发生变化时，此回调提供通知。

当发生以下情况之一时， ** \\ 回调 \\ PowerState**回调对象将提供通知：

-   系统从交流电源切换到直流电电源，反之亦然。

-   系统电源策略因用户或应用程序请求而更改。

-   即将过渡到系统睡眠或关闭状态。 驱动程序可以请求通知，以便可以将代码锁定到内存中，以便于关闭。 在电源管理器发送系统设置-power IRP 之前，会通知回调例程。

向系统添加新处理器时， ** \\ 回调 \\ ProcessorAdd**回调会提供通知。

若要使用系统定义的回调，驱动程序将使用回调的名称初始化属性块 ([**InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)) ，然后打开 ([**ExCreateCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)) 的回调对象，就像为驱动程序定义的回调那样。 驱动程序不应请求创建回调对象。

使用 **ExCreateCallback**返回的句柄，驱动程序将调用 [**ExRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exregistercallback) 来注册通知例程，并将指向任意上下文的指针和指向其例程的指针传递到该例程。 驱动程序可以随时注册其回调例程。 当出现指定的条件时，系统会调用已注册的回调例程，以 IRQL &lt; = 调度 \_ 级别。

当驱动程序不再需要通知时，它应调用 [**ExUnregisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exunregistercallback) 以从注册的回调列表中删除其回调例程，并删除其对回调对象的引用。

 

