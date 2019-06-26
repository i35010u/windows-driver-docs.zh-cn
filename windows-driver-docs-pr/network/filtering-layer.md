---
title: 筛选层
description: 筛选层
ms.assetid: db2fd1dc-c080-4f12-8138-7e66c74adacd
keywords:
- 筛选层 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c95414c2dc2483d7d7f62ed89f9a21d87d0754d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353334"
---
# <a name="filtering-layer"></a>筛选层


一个*筛选层*是个网络数据传递给 TCP/IP 网络堆栈中的点[筛选器引擎](filter-engine.md)为与当前组筛选器相匹配。 由一个唯一标识网络堆栈中的每个筛选层[筛选层标识符](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-layer-identifiers)。

当[筛选器](filter.md)添加到筛选器引擎中，添加在指定的筛选层，它将筛选器的网络数据。 特定[数据字段](https://docs.microsoft.com/windows-hardware/drivers/network/data-field-identifiers)都可用在处理每个筛选层的已添加到筛选器引擎在该图层的筛选器。 如果筛选器引擎传递到的网络数据[标注](callout.md)以进行其他处理，它包括这些数据字段和任何[元数据](https://docs.microsoft.com/windows-hardware/drivers/network/metadata-fields)位于该筛选层。

[运行时筛选层标识符](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers)(FWPS\_*XXX*) 使用的内核模式标注驱动程序。 [管理筛选层标识符](https://docs.microsoft.com/windows-hardware/drivers/network/management-filtering-layer-identifiers)(FWPM\_*XXX*) 由**Fwpm * Xxx*** 交互使用基本筛选引擎 (BFE) 从任何一种用户模式的函数或内核模式 (例如， [ **FwpmFilterAdd0**](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0))。

FWPS 数据类型为小于对应的 FWPM: FWPM 筛选层标识符是 Guid （128 位），而是筛选层标识符 FWPS [ **Luid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/igpupvdev/ns-igpupvdev-_luid)（64 位）。 FWPS 数据类型的较小大小可以提高系统性能，因为整数比较速度要快于实时流量的 GUID 比较和内核内存更有效地处理 FWPS 类型。

 

 





