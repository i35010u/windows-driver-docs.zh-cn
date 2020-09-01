---
title: 中间驱动程序中的状态指示
description: 中间驱动程序中的状态指示
ms.assetid: be8d50f9-4a8d-4f3c-a507-e64dedff9a3e
keywords:
- 中间驱动程序 WDK 网络，状态指示
- NDIS 中间驱动程序 WDK，状态指示
- 状态指示 WDK 网络，中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbe5a85312dbf87588362f8ba8331a15bda25f6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214332"
---
# <a name="status-indications-in-an-intermediate-driver"></a>中间驱动程序中的状态指示





中间驱动程序中状态指示的实现与协议驱动程序中的实现几乎完全相同。 有关中间驱动程序状态指示的详细信息，请参阅 [协议驱动程序中的状态指示](status-indications-in-a-protocol-driver.md)。

当中间驱动程序收到状态指示时，它可以通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)指示更高级别驱动程序的状态指示。 中间驱动程序应根据特定设计要求，向过量驱动程序指示状态更改。

 

