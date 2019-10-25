---
title: 使用系统定义的回调对象
description: 使用系统定义的回调对象
ms.assetid: 1f1a2fc1-e698-41f7-84e4-9db091def690
keywords:
- 回叫对象 WDK 内核
- 系统定义的回叫对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e5686dd3a37f86e8a2a8db7f87d162eac5c785e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836023"
---
# <a name="using-a-system-defined-callback-object"></a>使用系统定义的回调对象





系统为驱动程序使用定义了三个回调对象：

**\\回调\\SetSystemTime**

**\\回调\\PowerState**

**\\回调\\ProcessorAdd**

使用系统时间的驱动程序（例如，文件系统驱动程序）可能会注册 **\\回调\\SetSystemTime**回调对象。 当系统时间发生变化时，此回调提供通知。

当发生以下情况之一时， **\\回调\\PowerState**回调对象提供通知：

-   系统从交流电源切换到直流电电源，反之亦然。

-   系统电源策略因用户或应用程序请求而更改。

-   即将过渡到系统睡眠或关闭状态。 驱动程序可以请求通知，以便可以将代码锁定到内存中，以便于关闭。 在电源管理器发送系统设置-power IRP 之前，会通知回调例程。

将新处理器添加到系统时， **\\回调\\ProcessorAdd**回调提供通知。

若要使用系统定义的回调，驱动程序将使用回调的名称初始化属性块（[**InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)），然后打开回调对象（[**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)），就像驱动程序定义的回调一样。 驱动程序不应请求创建回调对象。

使用**ExCreateCallback**返回的句柄，驱动程序将调用[**ExRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exregistercallback)来注册通知例程，并将指向任意上下文的指针和指向其例程的指针传递到该例程。 驱动程序可以随时注册其回调例程。 当指定的条件出现时，系统将以 IRQL&lt;= 调度\_级别调用注册的回调例程。

当驱动程序不再需要通知时，它应调用[**ExUnregisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exunregistercallback)以从注册的回调列表中删除其回调例程，并删除其对回调对象的引用。

 

 




