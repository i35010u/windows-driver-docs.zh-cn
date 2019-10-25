---
title: 调用 PCMCIA_INTERFACE_STANDARD 接口例程
description: 调用 PCMCIA_INTERFACE_STANDARD 接口例程
ms.assetid: 468d2037-a7d5-4851-9f41-d1e6c9006750
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a1c5d4f8a58b65c555fc8ea7bd2310badc506f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837732"
---
# <a name="calling-a-pcmcia_interface_standard-interface-routine"></a>\_标准接口例程调用 PCMCIA\_接口





本部分介绍如何\_标准接口例程调用 PCMCIA\_接口。

驱动程序从 PCMCIA 总线驱动程序获取[pcmcia\_接口\_标准接口内存卡例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)结构后，该驱动程序可以调用接口例程。

每个接口例程都需要一个上下文指针。 驱动程序必须使用 PCMCIA 总线驱动程序在 PCMCIA\_接口\_标准结构中返回的**上下文**成员值。 如果上下文指针无效，则系统行为未定义，并且系统可能会暂停。

PCMCIA\_接口\_标准接口例程可按 IRQL &lt;= 调度\_级别进行调用。 为了维护整体系统性能，强烈建议驱动程序以 IRQL &lt; 调度\_级别调用这些例程。 在 IRQL 调度\_级别调用接口例程可能会导致调用方在很长一段时间内阻止系统操作。

 

 





