---
title: 中间驱动程序中的状态指示
description: 中间驱动程序中的状态指示
keywords:
- 中间驱动程序 WDK 网络，状态指示
- NDIS 中间驱动程序 WDK，状态指示
- 状态指示 WDK 网络，中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 467c94f8e7ff959e9f57d39b691c9a0b3d4caac1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838721"
---
# <a name="status-indications-in-an-intermediate-driver"></a>中间驱动程序中的状态指示





中间驱动程序中状态指示的实现与协议驱动程序中的实现几乎完全相同。 有关中间驱动程序状态指示的详细信息，请参阅 [协议驱动程序中的状态指示](status-indications-in-a-protocol-driver.md)。

当中间驱动程序收到状态指示时，它可以通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)指示更高级别驱动程序的状态指示。 中间驱动程序应根据特定设计要求，向过量驱动程序指示状态更改。

 

