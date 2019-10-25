---
title: 框架对象属性
description: 框架对象属性
ms.assetid: d95a7f51-fe22-4cd6-8c46-6d571f7d9169
keywords:
- framework 对象 WDK KMDF，属性
- 属性 WDK KMDF
- get 方法 WDK KMDF
- set 方法 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29e2bfe3c28fbb987e00ad4e0c2c8bbc7045c921
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845137"
---
# <a name="framework-object-properties"></a>框架对象属性





大多数框架对象都包含属性集。 属性表示可用于驱动程序的信息。 从驱动程序的角度来看，某些属性是只读的，而有些则是可读/写的。

对于每个可读属性，框架定义一个 "get" 方法，驱动程序可调用该[方法](framework-object-methods.md)来检索属性的值。 每个 "get" 方法返回属性的当前值。

对于每个可写属性，框架定义一个 "set" 方法，驱动程序可调用该方法来修改属性的值。 驱动程序提供属性的新值作为 "set" 方法的输入参数。

例如，框架设备对象定义了两个方法： [**WdfDeviceGetDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestate)和[**WdfDeviceSetDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)，驱动程序可调用该方法来获取或设置设备的即插即用（PnP）状态。

 

 





