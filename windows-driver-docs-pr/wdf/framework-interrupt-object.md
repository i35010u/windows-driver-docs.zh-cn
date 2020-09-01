---
title: 框架中断对象
description: 框架中断对象
ms.assetid: FA2B8C11-69D2-4A9E-8F57-C7295DA4EE44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69ecc100f6e0135c18e8eb562e2a347de11c266b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192753"
---
# <a name="framework-interrupt-object"></a>框架中断对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架中断对象由 [**IWDFInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt) 接口向驱动程序公开。 它表示硬件中断。 中断对象是 [UMDF 设备对象](framework-device-object.md)的子项。 驱动程序可以调用 [**IWDFDevice3：： CreateInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt) 方法来创建中断对象。

当驱动程序创建中断时，它们可以为该框架所调用的回调函数提供接口，以便在与接口相关的事件发生时通知驱动程序。 有关详细信息，请参阅 [UMDF 中断对象事件回调函数](/windows-hardware/drivers/ddi/wudfddi/)。

有关中断对象的详细信息，请参阅 [处理中断](handling-interrupts.md)。

 

