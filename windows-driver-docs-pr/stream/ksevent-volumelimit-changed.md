---
title: 'KSEVENT \_ VOLUMELIMIT \_ 更改 (流) '
description: KSEVENT \_ VOLUMELIMIT \_ CHANGED 事件将卷更改操作从内核模式驱动程序传播到用户模式。
ms.assetid: C4CB9E8A-A0B6-48E1-B020-EA6A0768AE05
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
ms.openlocfilehash: de809cad31483fdf970592eb62790db9de5ee765
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192181"
---
# <a name="ksevent_volumelimit_changed-stream"></a>KSEVENT \_ VOLUMELIMIT \_ 更改 (流) 

**KSEVENT \_ VOLUMELIMIT \_ CHANGED**事件将卷更改操作从内核模式驱动程序传播到用户模式。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 目标 | 事件描述符类型 | 事件值类型 |
|--|--|--|--|--|
| 否 | 是 | Pin | [**KSE_NODE**](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node) | [**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata) |