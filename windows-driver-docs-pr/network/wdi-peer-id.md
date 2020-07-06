---
title: WDI_PEER_ID
description: 本主题介绍 WDI 微型端口驱动程序的 WDI_PEER_ID 数据类型。
ms.assetid: 2D8700BC-7FED-4343-AC3F-8C43B0BE40FF
keywords:
- WDI_PEER_ID，WDK WDI_PEER_ID 网络驱动程序
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb25861a52f1d83ab9ce8f93ec7fafdd1e6f0118
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967892"
---
# <a name="wdi_peer_id"></a>WDI_PEER_ID

WDI_PEER_ID 数据类型是定义对等 ID 的 UINT16 值。

```c++
typedef UINT16 WDI_PEER_ID;
```

## <a name="remarks"></a>备注

如果要指定任何对等（通配符），可以使用 WDI_PEER_ANY （0xFFFF）值。

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi


