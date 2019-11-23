---
title: 标头版本的 NDIS 支持概述
description: 标头版本的 NDIS 支持概述
ms.assetid: f73baf8d-f6da-486c-b0e2-c3c57aeab269
keywords:
- NDIS 版本信息 WDK，结构要求
- NDIS 版本信息 WDK，头成员
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ef790e46a20d284d924b0053c74b2fec20b253
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843736"
---
# <a name="overview-of-ndis-support-for-header-versions"></a>标头版本的 NDIS 支持概述





许多 NDIS 结构都包含结构版本信息。 NDIS 或 NDIS 驱动程序根据每个结构的需要初始化此类结构中的**标头**成员。 NDIS 驱动程序应检查每个结构中的版本信息（如果有），然后再访问结构成员。

**标头**成员是一个[**NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构。 此结构包含包含**标头**成员的结构的修订号、类型和大小。

包含**标头**成员的结构满足以下要求：

-   如果将新信息添加到新的 NDIS 版本的成员列表中，结构将具有新的修订值。 例如，如果该结构的 NDIS 6.1 版本在成员列表、联合或位掩码末尾有新成员，则它将具有不同于 NDIS 6.0 版本的修订值。

-   结构更改后，结构的后一版本大小可以等于或大于结构的早期版本大小，但不会变得更小。 如果新大小大于早期版本的大小，则在成员列表的末尾添加新成员。

-   如果早期版本的信息仍然有效并已完成，则结构将只有新的修订版本。 也就是说，新版本的结构包含较早版本成员的超集。
    **请注意**  如果无法满足上述任何条件，NDIS 将提供新的结构，新的名称替换现有的结构，而不是提供现有结构的修改版本。

     

-   NDIS 驱动程序应始终使用预定义的修订值。 NDIS 以 Xxx 格式提供此类定义\_修订版\_Nn，NDIS\_SIZEOF\_Xxx\_修订版\_Nn，用于[**ndis\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)的**修订**和**大小**成员分别. 另外，Xxx 代表结构的名称，Nn 是修订号。 例如，Ndis\_筛选器的第一个修订版本和大小[ **\_部分\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_partial_characteristics)结构为 NDIS\_FILTER\_部分\_特征\_修订版\_1 和NDIS\_SIZEOF\_筛选器\_部分\_特征分别\_修订版\_1。

-   **标头**值必须与**标头**的大小一致。修订值。 也就是说，如果**修订版**成员包含 XXX\_修订版\_1，则**Size**成员值必须等于或大于 NDIS\_SIZEOF\_Xxx\_修订版\_1。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






