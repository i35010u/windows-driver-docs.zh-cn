---
title: 'KSEVENT \_ VOLUMELIMIT \_ 更改 (流) '
description: KSEVENT \_ VOLUMELIMIT \_ CHANGED 事件将卷更改操作从内核模式驱动程序传播到用户模式。
keywords:
- KSEVENT_VOLUMELIMIT_CHANGED 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_VOLUMELIMIT_CHANGED
api_type:
- NA
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: d921960dda224581f03c169845b10ea4e3cef0a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813413"
---
# <a name="ksevent_volumelimit_changed-stream"></a>KSEVENT \_ VOLUMELIMIT \_ 更改 (流) 

**KSEVENT \_ VOLUMELIMIT \_ CHANGED** 事件将卷更改操作从内核模式驱动程序传播到用户模式。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 事件描述符类型 | 事件值类型 |
|--|--|--|--|--|
| 否 | 是 | Pin | [**KSE_NODE**](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node) | [**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata) |
