---
title: WDI_PEER_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_PEER_ID 数据类型。
ms.assetid: 2D8700BC-7FED-4343-AC3F-8C43B0BE40FF
keywords:
- WDI_PEER_ID，WDK WDI_PEER_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12cebc10a70f34dff7d43055249e53d90d5a0b47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385290"
---
# <a name="wdipeerid"></a>WDI_PEER_ID

WDI_PEER_ID 数据类型是一个 UINT16 值，定义对等方 id。

```c++
typedef UINT16 WDI_PEER_ID;
```

## <a name="remarks"></a>备注

如果你想要指定任何对等 （通配符），可以使用 WDI_PEER_ANY (0xFFFF) 值。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |

