---
title: 使用 NDIS 6.20 数据结构
description: 使用 NDIS 6.20 数据结构
ms.assetid: 19810a7c-91c1-4014-a364-2819d743627d
keywords:
- NDIS 6.20 WDK，数据结构
- 数据结构 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdaad950481937d5a9a68af017c9c1b96130b6c8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842986"
---
# <a name="using-ndis-620-data-structures"></a>使用 NDIS 6.20 数据结构





NDIS 可支持同一数据结构的多个版本。 使用更新结构的 NDIS 6.20 和更高版本的驱动程序必须在该结构的**标头**结构中[ **\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构中（如果有）报告正确的**修订版**成员和**Size**成员\_值（如果有），当驱动程序初始化 NDIS 6.20 数据结构时。

**请注意**  确定正确的版本和大小信息，请参阅每个包含**标头**成员的结构的参考页。 对于包含**标头**成员并且已针对 ndis 6.20 更新的结构，其引用页包含 ndis 6.20 和更高版本的驱动程序的新信息。 如果没有针对 NDIS 6.20 的结构的更新，则为 NDIS 6.0 或 NDIS 6.1 驱动程序提供的信息也适用于 NDIS 6.20 和更高版本的驱动程序。

 

 

 





