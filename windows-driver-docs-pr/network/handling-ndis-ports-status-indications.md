---
title: 处理 NDIS 端口状态指示
description: 处理 NDIS 端口状态指示
ms.assetid: ba3794de-b17e-4878-a65e-6c9f5f8ebbbc
keywords:
- WDK NDIS，状态指示端口
- NDIS WDK，状态指示端口
- 状态指示 WDK 网络 NDIS 端口
- 端口状态 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187f81134460364eb5119f7cafb8686f6b213f69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379805"
---
# <a name="handling-ndis-ports-status-indications"></a>处理 NDIS 端口状态指示





如果 NDIS 端口的状态指示的源，应使用微型端口驱动程序**PortNumber**中的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构，以指定源端口。 微型端口驱动程序永远不会指示非活动状态的端口的状态。

微型端口驱动程序应使用[ **NDIS\_状态\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)状态指示，指示在 NDIS 端口的状态更改。 获取此状态指示，微型端口驱动程序必须设置的端口号**PortNumber**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构。 **StatusBuffer**成员的 NDIS\_状态\_指示结构包含一个指向[ **NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)结构。

 

 





