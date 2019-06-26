---
title: 框架对象属性
description: 框架对象属性
ms.assetid: d95a7f51-fe22-4cd6-8c46-6d571f7d9169
keywords:
- framework 对象 WDK KMDF，属性
- WDK KMDF 属性
- 获取 WDK KMDF 方法
- set 方法 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0903785c1f69c7e1bcfd97369c2802538bff96c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384448"
---
# <a name="framework-object-properties"></a>框架对象属性





大多数 framework 对象包含属性的集。 属性表示可供一个驱动程序的信息。 从驱动程序的角度来看，某些属性是只读的一些是读/写。

对于每个可读的属性，该框架定义"get"[方法](framework-object-methods.md)驱动程序可以调用以检索属性的值。 每个"get"方法返回的属性的当前值。

对于每个可写属性，该框架定义驱动程序可以调用来修改属性的值的"set"方法。 驱动程序提供"set"方法的输入参数作为属性的新值。

例如，framework 设备对象定义了两个方法： [ **WdfDeviceGetDeviceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestate)并[ **WdfDeviceSetDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)，驱动程序可以调用要获取或设置设备的插 (PnP) 状态。

 

 





