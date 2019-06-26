---
title: 用户拔出设备
description: 用户拔出设备
ms.assetid: d0c8fd6d-b356-4048-aa97-ebe331d23361
keywords:
- 电源管理方案 WDK UMDF，拔出该设备
- 拔出设备方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36a1766d8a27a380ee95f0f01656324254c57a89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385330"
---
# <a name="a-user-unplugs-a-device"></a>用户拔出设备


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

运行系统时，用户可以删除设备中的以下项之一通过两种方式： 通过*有序地删除*，这意味着用户通知系统是否要删除 （例如，通过使用拔出或弹出设备硬件计划）;或由*感到惊讶删除*，这意味着用户而不通知系统断开设备。 如果在总线支持在意外删除 (例如，USB)，设备的驱动程序必须能够处理设备的突然消失。

<a href="" id="orderly-removal-------"></a>**有序地删除**   
用户请求删除通过使用系统的拔出或弹出硬件程序，通过使用设备管理器禁用设备，或通过将推送无可退出设备的弹出按钮。 该框架允许在设备中删除或禁用，除非已经提供了驱动程序[ **IPnpCallback::OnQueryRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-onqueryremove)回调函数和回调函数已禁止删除。

下图显示在电源关闭和删除的 UMDF 回调序列。 在序列图顶部开始工作电源状态 (D0) 的设备。

![设备电源关闭和有序地删除序列 umdf 驱动程序](images/umdf-powerdown-sequence.png)

<a href="" id="surprise-removal-------"></a>**意外删除**   
在此方案中，用户意外断开设备。 在意外删除序列中，调用 UMDF [ **IPnpCallback::OnSurpriseRemoval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-onsurpriseremoval)回调，从而通知已意外删除设备驱动程序。 此回叫不能保证出现在任何特定顺序与删除序列中的其他回调。

通常情况下，该驱动程序应避免访问删除路径中的硬件。 如果尝试访问硬件将无限期等待该发送程序已超时。 下图显示了 UMDF 驱动程序的意外删除序列。

![umdf 驱动程序的意外删除序列](images/umdf-surprise-removal-sequence.png)

 

 





