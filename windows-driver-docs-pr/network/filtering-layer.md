---
title: 筛选层
description: 筛选层
ms.assetid: db2fd1dc-c080-4f12-8138-7e66c74adacd
keywords:
- 筛选层 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3790778a96eed061c961f51df14e90c58f81b4b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540411"
---
# <a name="filtering-layer"></a>筛选层


一个*筛选层*是个网络数据传递给 TCP/IP 网络堆栈中的点[筛选器引擎](filter-engine.md)为与当前组筛选器相匹配。 由一个唯一标识网络堆栈中的每个筛选层[筛选层标识符](https://msdn.microsoft.com/library/windows/hardware/ff549947)。

当[筛选器](filter.md)添加到筛选器引擎中，添加在指定的筛选层，它将筛选器的网络数据。 特定[数据字段](https://msdn.microsoft.com/library/windows/hardware/ff546312)都可用在处理每个筛选层的已添加到筛选器引擎在该图层的筛选器。 如果筛选器引擎传递到的网络数据[标注](callout.md)以进行其他处理，它包括这些数据字段和任何[元数据](https://msdn.microsoft.com/library/windows/hardware/ff559174)位于该筛选层。

[运行时筛选层标识符](https://msdn.microsoft.com/library/windows/hardware/ff570731)(FWPS\_*XXX*) 使用的内核模式标注驱动程序。 [管理筛选层标识符](https://msdn.microsoft.com/library/windows/hardware/ff557101)(FWPM\_*XXX*) 由**Fwpm * Xxx*** 交互使用基本筛选引擎 (BFE) 从任何一种用户模式的函数或内核模式 (例如， [ **FwpmFilterAdd0**](https://msdn.microsoft.com/library/windows/desktop/aa364046))。

FWPS 数据类型为小于对应的 FWPM: FWPM 筛选层标识符是 Guid （128 位），而是筛选层标识符 FWPS [ **Luid**](https://msdn.microsoft.com/library/windows/hardware/ff557080)（64 位）。 FWPS 数据类型的较小大小可以提高系统性能，因为整数比较速度要快于实时流量的 GUID 比较和内核内存更有效地处理 FWPS 类型。

 

 





