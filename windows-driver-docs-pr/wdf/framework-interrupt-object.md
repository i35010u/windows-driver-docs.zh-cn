---
title: 框架中断对象
description: 框架中断对象
ms.assetid: FA2B8C11-69D2-4A9E-8F57-C7295DA4EE44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b40691410ab820dc7df17235a40068c9540c251f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843168"
---
# <a name="framework-interrupt-object"></a>框架中断对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架中断对象由[**IWDFInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt)接口向驱动程序公开。 它表示硬件中断。 中断对象是[UMDF 设备对象](framework-device-object.md)的子项。 驱动程序可以调用[**IWDFDevice3：： CreateInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)方法来创建中断对象。

当驱动程序创建中断时，它们可以为该框架所调用的回调函数提供接口，以便在与接口相关的事件发生时通知驱动程序。 有关详细信息，请参阅[UMDF 中断对象事件回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/)。

有关中断对象的详细信息，请参阅[处理中断](handling-interrupts.md)。

 

 





