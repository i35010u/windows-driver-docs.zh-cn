---
title: 查询端口状态
description: 查询端口状态
ms.assetid: 3659d99b-1bbd-453c-8a56-b968d1748c1f
keywords:
- 端口状态 WDK NDIS
- 查询 NDIS 端口状态
- 端口 WDK NDIS OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52ab66d44bf1fbc231531525f8cca387fb2b1de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563236"
---
# <a name="querying-the-port-state"></a>查询端口状态





过量驱动程序可以发出[OID\_代\_端口\_状态](https://msdn.microsoft.com/library/windows/hardware/ff569624)OID 查询请求以获取中指定的端口的当前状态**PortNumber**成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。 NDIS 接收端口的状态信息中[ **NDIS\_端口\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566791)结构。

OID\_GEN\_端口\_NDIS 6.0 和更高版本中支持状态 OID。

过量驱动程序应避免使用 OID\_GEN\_端口\_状态在可能的情况，应依赖于[ **NDIS\_状态\_端口\_状态** ](https://msdn.microsoft.com/library/windows/hardware/ff567415)状态指示。 有关端口相关的状态指示的详细信息，请参阅[处理 NDIS 端口状态指示](handling-ndis-ports-status-indications.md)。

如果 OID\_GEN\_端口\_状态查询成功，则将 NDIS 返回中的端口状态信息[ **NDIS\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566800)结构。

 

 





