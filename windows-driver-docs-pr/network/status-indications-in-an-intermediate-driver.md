---
title: 中间驱动程序中的状态指示
description: 中间驱动程序中的状态指示
ms.assetid: be8d50f9-4a8d-4f3c-a507-e64dedff9a3e
keywords:
- 状态指示中间驱动程序 WDK 网络
- NDIS 中间层驱动程序 WDK，状态指示
- 状态指示 WDK 网络连接、 中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58ecc228e539d4b6fc41891ff6befe65dc401963
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383608"
---
# <a name="status-indications-in-an-intermediate-driver"></a>中间驱动程序中的状态指示





状态指示中间驱动程序中的实现与协议驱动程序中实现几乎完全相同。 有关中间驱动程序状态指示的详细信息，请参阅[协议驱动程序中的状态指示](status-indications-in-a-protocol-driver.md)。

当中间驱动程序收到的状态指示时，它可以通过调用指示最多的更高级别的驱动程序的状态指示[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)。 中间的驱动程序应指示状态将更改为根据其特定的设计要求基础驱动程序。

 

 





