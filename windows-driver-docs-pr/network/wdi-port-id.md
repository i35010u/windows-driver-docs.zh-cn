---
title: WDI_PORT_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_PORT_ID 数据类型。
keywords:
- WDI_PORT_ID，WDK WDI_PORT_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98ad9d8ede43c674ea21c4f3c270f7a4c6761603
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822085"
---
# <a name="wdi_port_id"></a>WDI_PORT_ID

WDI_PORT_ID 的数据类型是一个定义端口 ID 的 UINT16 值。

```c++
typedef UINT16 WDI_PORT_ID;
```

## <a name="remarks"></a>备注

如果要指定 (通配符) 的任何端口，则可以使用 WDI_PORT_ANY (0xFFFF) 值。

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi


