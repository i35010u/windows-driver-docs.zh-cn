---
title: 框架中断对象
description: 框架中断对象
ms.assetid: FA2B8C11-69D2-4A9E-8F57-C7295DA4EE44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec7f4a83b88e801d217216703c04431b02c182f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568573"
---
# <a name="framework-interrupt-object"></a>框架中断对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework 中断对象公开到由驱动程序[ **IWDFInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451283)接口。 它表示的硬件中断。 中断对象的子级[UMDF 设备对象](framework-device-object.md)。 驱动程序可以调用[ **IWDFDevice3::CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)方法来创建一个中断对象。

当驱动程序创建时中断时，他们可以与框架相关的接口的事件发生时通知该驱动程序调用的回调函数提供接口。 有关详细信息，请参阅[UMDF 中断对象事件的回调函数](https://msdn.microsoft.com/library/windows/hardware/hh463979)。

有关中断对象的详细信息，请参阅[处理中断](handling-interrupts.md)。

 

 





