---
title: 标头版本的 NDIS 支持概述
description: 标头版本的 NDIS 支持概述
keywords:
- NDIS 版本信息 WDK，结构要求
- NDIS 版本信息 WDK，头成员
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45929c5c8f47d4fb832316e0c4b852ffe8dab3c1
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247856"
---
# <a name="overview-of-ndis-support-for-header-versions"></a>标头版本的 NDIS 支持概述





许多 NDIS 结构都包含结构版本信息。 NDIS 或 NDIS 驱动程序根据每个结构的需要初始化此类结构中的 **标头** 成员。 NDIS 驱动程序应检查每个结构中的版本信息（如果有），然后再访问结构成员。

**标头** 成员是一个 [**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/objectheader/ns-objectheader-ndis_object_header)结构。 此结构包含包含 **标头** 成员的结构的修订号、类型和大小。

包含 **标头** 成员的结构满足以下要求：

-   如果将新信息添加到新的 NDIS 版本的成员列表中，结构将具有新的修订值。 例如，如果该结构的 NDIS 6.1 版本在成员列表、联合或位掩码末尾有新成员，则它将具有不同于 NDIS 6.0 版本的修订值。

-   结构更改后，结构的后一版本大小可以等于或大于结构的早期版本大小，但不会变得更小。 如果新大小大于早期版本的大小，则在成员列表的末尾添加新成员。

-   如果早期版本的信息仍然有效并已完成，则结构将只有新的修订版本。 也就是说，新版本的结构包含较早版本成员的超集。
    **注意**  如果无法满足上述任何条件，NDIS 将提供新的结构，新的名称替换现有的结构，而不是提供现有结构的修订版本。

     

-   NDIS 驱动程序应始终使用预定义的修订值。 \_ \_ \_ 对于每 \_ \_ \_ 个 [**Ndis \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/objectheader/ns-objectheader-ndis_object_header)的 **修订** 和 **大小** 成员，ndis 在 Xxx 修订版 nn 和 ndis SIZEOF Xxx 修订 nn 形式提供此类定义。 另外，Xxx 代表结构的名称，Nn 是修订号。 例如， [**ndis \_ 筛选器 \_ 分部 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_partial_characteristics) 结构的第一次修订版本的修订号和大小分别为 ndis \_ 筛选器 \_ 部分 \_ 特征 \_ 修订 \_ 1 和 ndis \_ SIZEOF \_ 筛选 \_ 部分 \_ 特征 \_ 修订 \_ 1。

-   **标头** 值必须与 **标头** 的大小一致。修订值。 也就是说，如果 **修订** 成员包含 Xxx \_ 版本 \_ 1，则 **Size** 成员值必须等于或大于 NDIS \_ SIZEOF \_ Xxx \_ 版本 \_ 1。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

