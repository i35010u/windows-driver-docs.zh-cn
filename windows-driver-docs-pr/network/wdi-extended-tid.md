---
title: WDI_EXTENDED_TID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_EXTENDED_TID 数据类型。
ms.assetid: C7ECB1BD-CB4A-4FD7-8222-9C9E25C15910
keywords:
- WDI_EXTENDED_TID，WDK WDI_EXTENDED_TID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6654123110081e749b939e1d147f8685a7a16b60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330499"
---
# <a name="wdiextendedtid"></a>WDI_EXTENDED_TID

WDI_EXTENDED_TID 数据类型是一个定义通信标识符 (TID) 的 UINT8 值。

```c++
typedef UINT8 WDI_EXTENDED_TID;
```

## <a name="remarks"></a>备注

可能的值如下：

| ReplTest1 | 描述 |
| --- | --- |
| 0-15 | 802.11 Tid |
| 16 (WDI_EXT_TID_NON_QOS) | 非 QoS 数据 |
| 17-24 | 保留以用于 IHV 注入框架。 与扩展 TID 间隔 17 24 中的帧被视为 17 日至 24 日在相同间隔内的优先级高于具有较小的扩展 TID。 |
| 25-30 | 未使用的值 |
| 31 (WDI_EXT_TID_UNKNOWN) | 未指定未知 / |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |

