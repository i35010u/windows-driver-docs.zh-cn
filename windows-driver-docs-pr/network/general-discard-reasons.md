---
title: 常规的放弃原因
description: 本部分描述了 Windows 筛选平台标注驱动程序的常规的放弃原因。
ms.assetid: 8b2d9028-a32e-42bf-b1ba-ab029bf47d71
keywords:
- 常规的放弃原因网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb3fb24d49d5159a4c4b596813cd49c8d9ee08bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519746"
---
# <a name="general-discard-reasons"></a>常规的放弃原因

标识符，则会丢弃数据由筛选器引擎的可能原因如下所示。 这些标识符是 Fwpstypes.h 中定义的 FWPS_GENERAL_DISCARD_REASON 枚举中的常量值。

| 放弃原因标识符 | 放弃原因说明 |
| --- | --- |
| FWPS_DISCARD_FIREWALL_POLICY | 从筛选决策返回 FWP_ACTION_BLOCK 操作。 |
| FWPS_DISCARD_IPSEC | 保留。 |

