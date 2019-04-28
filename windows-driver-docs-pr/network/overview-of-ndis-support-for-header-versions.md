---
title: 标头版本的 NDIS 支持概述
description: 标头版本的 NDIS 支持概述
ms.assetid: f73baf8d-f6da-486c-b0e2-c3c57aeab269
keywords:
- NDIS 版本信息 WDK，结构要求
- NDIS 版本信息 WDK，标头成员
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e202b391daab20778cbbe2bfbe28ee02a986930
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348089"
---
# <a name="overview-of-ndis-support-for-header-versions"></a>标头版本的 NDIS 支持概述





许多 NDIS 结构，包括结构版本信息。 NDIS 或 NDIS 驱动程序初始化**标头**中根据需要为每个结构的此类结构的成员。 NDIS 驱动程序应检查的版本信息，如果有，他们访问结构成员的每个结构中。

**标头**成员是[ **NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)结构。 此结构包含修订号、 类型和大小的结构，其中包含**标头**成员。

包括的结构**标头**成员满足以下要求：

-   如果新信息添加到成员列表中新的 NDIS 版本，则结构将具有新的修订值。 例如，如果结构的 NDIS 6.1 版本具有新成员末尾的成员列表中，联合，或一个位掩码，它将具有不同版本值从 NDIS 6.0 版本。

-   结构发生更改后，结构的更高版本的修订版本的大小可以是等于或大于结构的更早的修订版本的大小，但它不会较小。 如果新大小大于较早的修订版本的大小，在成员列表末尾添加新成员。

-   如果早期的修订版本信息仍然有效且完整，结构将仅有的新修订版本。 也就是说，该结构的新版本包含较旧版本成员的超集。
    **请注意**  NDIS 不能满足任何上述条件，如果提供使用替换而不是提供现有结构的修订的版本的现有结构的新名称的新结构。

     

-   NDIS 驱动程序应始终使用预定义的修订值。 NDIS 提供此类定义在窗体 Xxx\_修订\_Nn 和 NDIS\_SIZEOF\_Xxx\_修订\_Nn，对于**修订**和**大小**的成员[ **NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)分别。 此外，Xxx 代表的结构的名称，Nn 的修订号。 例如，让修订版本和大小的第一个修订版[ **NDIS\_筛选器\_分部\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565544)结构是 NDIS\_筛选器\_分部\_特征\_修订\_1 和 NDIS\_SIZEOF\_筛选器\_部分\_特征\_修订\_1 分别。

-   **Header.Size**值必须是符合**Header.Revision**值。 也就是说，如果**修订**成员包含 Xxx\_修订\_1，**大小**成员值必须等于或大于 NDIS\_SIZEOF\_Xxx\_修订\_1。

## <a name="related-topics"></a>相关主题


[NDIS 版本的概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






