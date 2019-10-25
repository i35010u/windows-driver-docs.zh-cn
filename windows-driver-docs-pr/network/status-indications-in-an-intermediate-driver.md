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
ms.openlocfilehash: a8b5b9cab345edba69f1236bf883715140e45ea4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841825"
---
# <a name="status-indications-in-an-intermediate-driver"></a>中间驱动程序中的状态指示





中间驱动程序中状态指示的实现与协议驱动程序中的实现几乎完全相同。 有关中间驱动程序状态指示的详细信息，请参阅[协议驱动程序中的状态指示](status-indications-in-a-protocol-driver.md)。

当中间驱动程序收到状态指示时，它可以通过调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)指示更高级别驱动程序的状态指示。 中间驱动程序应根据特定设计要求，向过量驱动程序指示状态更改。

 

 





