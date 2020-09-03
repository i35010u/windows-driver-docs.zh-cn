---
title: 调用 PCMCIA_INTERFACE_STANDARD 接口例程
description: 调用 PCMCIA_INTERFACE_STANDARD 接口例程
ms.assetid: 468d2037-a7d5-4851-9f41-d1e6c9006750
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b47075432cf94570ae8ad3e8bea2bfbb6582a6c
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384811"
---
# <a name="calling-a-pcmcia_interface_standard-interface-routine"></a>调用 PCMCIA \_ 接口 \_ 标准接口例程





本部分介绍如何调用 PCMCIA \_ 接口 \_ 标准接口例程。

在驱动程序从 PCMCIA 总线驱动程序获取 [pcmcia \_ 接口 \_ 标准接口内存卡例程](/windows-hardware/drivers/ddi/index) 结构之后，驱动程序可以调用接口例程。

每个接口例程都需要一个上下文指针。 驱动程序必须使用 pcmcia **Context** \_ 接口标准结构中的 pcmcia 总线驱动程序返回的上下文成员值 \_ 。 如果上下文指针无效，则系统行为未定义，并且系统可能会暂停。

PCMCIA \_ 接口 \_ 标准接口例程可在 IRQL &lt; = 调度 \_ 级别调用。 为了维护整体系统性能，强烈建议驱动程序以 IRQL 调度级别调用这些例程 &lt; \_ 。 在 IRQL 调度级别调用接口例程 \_ 可能导致调用方在很长一段时间内阻止系统操作。

 

