---
title: 调用 PCMCIA_INTERFACE_STANDARD 接口例程
description: 调用 PCMCIA_INTERFACE_STANDARD 接口例程
ms.assetid: 468d2037-a7d5-4851-9f41-d1e6c9006750
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7a2ddc569b82b7a6a206c7bd6168e0213eddfe6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386199"
---
# <a name="calling-a-pcmciainterfacestandard-interface-routine"></a>调用 PCMCIA\_接口\_标准接口例程





本部分介绍如何调用 PCMCIA\_接口\_标准接口例程。

驱动程序将获取后[PCMCIA\_界面\_标准接口内存卡例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)结构从 PCMCIA 总线驱动程序，该驱动程序可以调用接口例程。

每个接口例程需要上下文指针。 该驱动程序必须使用**上下文**PCMCIA 中的 PCMCIA 总线驱动程序返回的成员值\_接口\_标准结构。 如果上下文指针不是有效的未定义的系统行为，而且系统可能会暂停。

PCMCIA\_接口\_标准接口例程可以调用在 IRQL &lt;= 调度\_级别。 若要维护系统的整体性能，强烈建议一个驱动程序，调用这些例程在 IRQL&lt;调度\_级别。 在 IRQL 调度调用接口例程\_级别可能会导致调用方的重要的一段时间内的块系统操作。

 

 





