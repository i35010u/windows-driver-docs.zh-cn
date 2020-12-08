---
title: WDI_FRAME_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_FRAME_ID 数据类型。
keywords:
- WDI_FRAME_ID，WDK WDI_FRAME_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96a7d19f139e8552c179358ca4de451f63711391
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833295"
---
# <a name="wdi_frame_id"></a>WDI_FRAME_ID

WDI_FRAME_ID 的数据类型是定义框架 ID 的 UINT16 值。 这只是一个标识符。 它不会传达有关帧顺序的信息。

```c++
typedef UINT16 WDI_FRAME_ID;
```

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi


