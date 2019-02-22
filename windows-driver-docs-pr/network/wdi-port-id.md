---
title: WDI_PORT_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_PORT_ID 数据类型。
ms.assetid: 16385F87-E3BE-4CCC-8E40-C4AAEA399964
keywords:
- WDI_PORT_ID，WDK WDI_PORT_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b5f33728e7ff3421ecfd2c36db9ee8d8378f80e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555763"
---
# <a name="wdiportid"></a>WDI_PORT_ID

WDI_PORT_ID 数据类型是一个 UINT16 值，定义一个端口 id。

```c++
typedef UINT16 WDI_PORT_ID;
```

## <a name="remarks"></a>备注

如果你想要指定任何端口 （通配符），可以使用 WDI_PORT_ANY (0xFFFF) 值。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 |
| 最低受支持的服务器 | Windows Server 2016 |
| 标头 | Dot11wdi.h |

