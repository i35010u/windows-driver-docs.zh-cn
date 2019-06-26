---
title: 使用系统定义的回调对象
description: 使用系统定义的回调对象
ms.assetid: 1f1a2fc1-e698-41f7-84e4-9db091def690
keywords:
- 回调对象 WDK 内核
- 系统定义的回调对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbfdde80eb93a862937c09c63d034c6e1f93ccf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385104"
---
# <a name="using-a-system-defined-callback-object"></a>使用系统定义的回调对象





系统定义驱动程序使用的三个回调的对象：

**\\Callback\\SetSystemTime**

**\\Callback\\PowerState**

**\\Callback\\ProcessorAdd**

使用系统时间 （例如，文件系统驱动程序） 的驱动程序可能注册，以便 **\\回调\\SetSystemTime**回调对象。 系统时间更改时，此回调提供通知。

**\\回调\\PowerState**发生下列情况之一时，回调对象提供的通知：

-   为 DC 电源，反之亦然，系统会从 AC 切换。

-   系统电源策略为用户或应用程序请求的结果的更改。

-   即将转换到系统睡眠或关闭状态。 驱动程序，以便它可以锁定代码到内存中预期的关闭请求通知。 电源管理器发送系统之前，将会通知回调例程集 power IRP。

**\\回调\\ProcessorAdd**回调时向系统添加新的处理器提供通知。

若要使用系统定义的回调，驱动程序初始化特性块 ([**InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes)) 具有回调的名称，然后打开回调对象 ([ **ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excreatecallback))，只需与驱动程序定义的回调。 驱动程序不应请求创建回调对象。

使用返回的句柄**ExCreateCallback**，驱动程序调用[ **ExRegisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exregistercallback)以注册通知例程中，将指针传递给任意上下文并指向其例程的指针。 驱动程序随时可以注册其回调例程。 系统指定的条件时，调用注册的回调例程在 IRQL&lt;= 调度\_级别。

当驱动程序不再需要通知时，则应调用[ **ExUnregisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exunregistercallback)若要从已注册的回调的列表中删除其回调例程并删除其对回调的引用对象。

 

 




