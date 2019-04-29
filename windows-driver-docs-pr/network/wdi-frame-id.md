---
title: WDI_FRAME_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_FRAME_ID 数据类型。
ms.assetid: 7D886BA2-EDD2-4770-948C-9C891D07EF58
keywords:
- WDI_FRAME_ID，WDK WDI_FRAME_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c88c7744c899f1f9ff3bb43d872757aad4b7b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367503"
---
# <a name="wdiframeid"></a>WDI_FRAME_ID

WDI_FRAME_ID 数据类型是一个 UINT16 值，定义一个帧 id。 这是仅一个标识符。 它不提供有关排序的帧的信息。

```c++
typedef UINT16 WDI_FRAME_ID;
```

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |

