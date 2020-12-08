---
title: 使用 NDIS 6.20 数据结构
description: 使用 NDIS 6.20 数据结构
keywords:
- NDIS 6.20 WDK，数据结构
- 数据结构 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76763f9785f65d35778cb8b9e717fd56c2b50a98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809899"
---
# <a name="using-ndis-620-data-structures"></a>使用 NDIS 6.20 数据结构





NDIS 可支持同一数据结构的多个版本。 当驱动程序初始化 NDIS 6.20 数据结构时，使用更新结构的 NDIS 6.20 和更高版本的驱动程序必须在结构的 **标头** 成员（如果有）中报告 [**正确的 \_ \_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) **修订版** 成员和 **Size** 成员值。

**注意**  若要确定正确的版本和大小信息，请参阅每个包含 **标头** 成员的结构的参考页。 对于包含 **标头** 成员并且已针对 ndis 6.20 更新的结构，其引用页包含 ndis 6.20 和更高版本的驱动程序的新信息。 如果没有针对 NDIS 6.20 的结构的更新，则为 NDIS 6.0 或 NDIS 6.1 驱动程序提供的信息也适用于 NDIS 6.20 和更高版本的驱动程序。

 

 

