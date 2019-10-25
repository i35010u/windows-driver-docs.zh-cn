---
title: 处理 NDIS 端口状态指示
description: 处理 NDIS 端口状态指示
ms.assetid: ba3794de-b17e-4878-a65e-6c9f5f8ebbbc
keywords:
- 端口 WDK NDIS，状态指示
- NDIS 端口 WDK，状态指示
- 状态指示 WDK 网络，NDIS 端口
- 端口状态 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b20cbb2a4303b18dc11cf26929c3a132a6bb702e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842583"
---
# <a name="handling-ndis-ports-status-indications"></a>处理 NDIS 端口状态指示





如果 NDIS 端口是状态指示的源，则微型端口驱动程序应使用[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构中的**PortNumber**成员来指定源端口。 微型端口驱动程序从不指示非活动端口的状态。

小型端口驱动程序应使用[**ndis\_状态\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)指示指示 NDIS 端口状态的更改。 对于此状态指示，微型端口驱动程序必须在[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**PortNumber**成员中设置端口号。 NDIS\_状态\_指示结构的**StatusBuffer**成员包含指向[**NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)结构的指针。

 

 





