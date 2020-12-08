---
title: WDI_PEER_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_PEER_ID 数据类型。
keywords:
- WDI_PEER_ID，WDK WDI_PEER_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05e1658cfb3c224b8f213d932c221acf54821bd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822091"
---
# <a name="wdi_peer_id"></a>WDI_PEER_ID

WDI_PEER_ID 数据类型是定义对等 ID 的 UINT16 值。

```c++
typedef UINT16 WDI_PEER_ID;
```

## <a name="remarks"></a>备注

如果要指定任何对等 (通配符) ，可以使用 WDI_PEER_ANY (0xFFFF) 值。

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi


