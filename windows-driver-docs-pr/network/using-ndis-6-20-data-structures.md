---
title: 使用 NDIS 6.20 数据结构
description: 使用 NDIS 6.20 数据结构
ms.assetid: 19810a7c-91c1-4014-a364-2819d743627d
keywords:
- NDIS 6.20 WDK，数据结构
- 数据结构 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83a02ed132802747945b64f334588f7767e9f80f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523174"
---
# <a name="using-ndis-620-data-structures"></a>使用 NDIS 6.20 数据结构





NDIS 可以支持多个版本的相同的数据结构。 NDIS 6.20 和更高版本的驱动程序，使用更新后的结构必须报告正确**修订**成员和**大小**中的成员值[ **NDIS\_对象\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566588)结构，它是在**标头**结构，如果有的话，当驱动程序初始化 NDIS 6.20 数据结构的成员。

**请注意**  来确定正确的版本和大小信息，请参阅每个结构，其中包含的参考页**标头**成员。 结构中包含的参考页**标头**成员的已更新和 NDIS 6.20 包括 NDIS 6.20 和更高版本的驱动程序的新信息。 如果不会更新到结构的 NDIS 6.20，NDIS 6.0 或 NDIS 6.1 驱动程序提供的信息也适用于 NDIS 6.20 和更高版本的驱动程序。

 

 

 





