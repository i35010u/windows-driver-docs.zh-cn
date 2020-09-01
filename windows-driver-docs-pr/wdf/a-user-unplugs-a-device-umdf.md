---
title: 用户将设备断开)  (
description: 用户拔出设备
ms.assetid: d0c8fd6d-b356-4048-aa97-ebe331d23361
keywords:
- 电源管理方案 WDK UMDF，拔出设备
- 拔出设备方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8fc8b6e03c71f1b85bbb4f4929107643d49d19
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189193"
---
# <a name="a-user-unplugs-a-device-umdf-1"></a>用户将设备断开)  (


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当系统运行时，用户可以通过以下两种方式之一删除设备：通过 *顺序删除*，这意味着用户会告知系统要删除设备 (例如，通过使用拔出或弹出硬件程序) ;或者是 *意外删除*，这意味着用户断开了设备，而无需通知系统。 如果总线支持意外删除 (例如，USB) ，则设备的驱动程序必须能够处理设备突然消失。

<a href="" id="orderly-removal-------"></a>**有序删除**   
用户使用系统的拔出或弹出硬件程序请求删除，方法是使用设备管理器禁用设备，或通过推送 ejectable 设备的弹出按钮。 框架允许删除或禁用设备，除非驱动程序提供了 [**IPnpCallback：： OnQueryRemove**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onqueryremove) 回调函数，并且回调函数已拒绝删除。

下图显示了在关机和删除中的 UMDF 回调的顺序。 序列从图形顶部开始，其设备处于工作电源状态 (D0) 。

![设备关机并有序删除 umdf 驱动程序的顺序](images/umdf-powerdown-sequence.png)

<a href="" id="surprise-removal-------"></a>**意外删除**   
在这种情况下，用户会意外断开设备。 在意外删除序列中，UMDF 将调用 [**IPnpCallback：： OnSurpriseRemoval**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onsurpriseremoval) 回调以通知驱动程序设备已被意外删除。 不保证在删除序列中具有其他回调的任何特定顺序执行此回调。

通常，驱动程序应避免访问删除路径中的硬件。 如果尝试无限期地访问硬件，则反射器会超时。 下图显示了 UMDF 驱动程序的意外删除序列。

![umdf 驱动程序的意外删除序列](images/umdf-surprise-removal-sequence.png)

 

