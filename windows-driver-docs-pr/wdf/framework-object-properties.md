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
ms.openlocfilehash: bcf8e9879929a8f08325ce6dbaa688c3c9920fd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543020"
---
# <a name="framework-object-properties"></a>框架对象属性





大多数 framework 对象包含属性的集。 属性表示可供一个驱动程序的信息。 从驱动程序的角度来看，某些属性是只读的一些是读/写。

对于每个可读的属性，该框架定义"get"[方法](framework-object-methods.md)驱动程序可以调用以检索属性的值。 每个"get"方法返回的属性的当前值。

对于每个可写属性，该框架定义驱动程序可以调用来修改属性的值的"set"方法。 驱动程序提供"set"方法的输入参数作为属性的新值。

例如，framework 设备对象定义了两个方法： [ **WdfDeviceGetDeviceState** ](https://msdn.microsoft.com/library/windows/hardware/ff545994)并[ **WdfDeviceSetDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff546884)，驱动程序可以调用要获取或设置设备的插 (PnP) 状态。

 

 





