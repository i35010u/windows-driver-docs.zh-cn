---
title: WDI_PORT_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_PORT_ID 数据类型。
ms.assetid: 16385F87-E3BE-4CCC-8E40-C4AAEA399964
keywords:
- WDI_PORT_ID，WDK WDI_PORT_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13b50d51671de17a4cc72b6a3fbc60a2c104aaba
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967920"
---
# <a name="wdi_port_id"></a>WDI_PORT_ID

WDI_PORT_ID 的数据类型是一个定义端口 ID 的 UINT16 值。

```c++
typedef UINT16 WDI_PORT_ID;
```

## <a name="remarks"></a>备注

如果要指定任何端口（通配符），可以使用 WDI_PORT_ANY （0xFFFF）值。

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi


