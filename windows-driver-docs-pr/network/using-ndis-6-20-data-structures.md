---
title: 使用 NDIS 6.20 数据结构
description: 使用 NDIS 6.20 数据结构
ms.assetid: 19810a7c-91c1-4014-a364-2819d743627d
keywords:
- NDIS 6.20 WDK，数据结构
- 数据结构 WDK NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e498c175ca2c855938321e605e9c24c3a1318ba
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215777"
---
# <a name="using-ndis-620-data-structures"></a>使用 NDIS 6.20 数据结构





NDIS 可支持同一数据结构的多个版本。 当驱动程序初始化 NDIS 6.20 数据结构时，使用更新结构的 NDIS 6.20 和更高版本的驱动程序必须在结构的**标头**成员（如果有）中报告[**正确的 \_ \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) **修订版**成员和**Size**成员值。

**注意**   若要确定正确的版本和大小信息，请参阅每个包含**标头**成员的结构的参考页。 对于包含 **标头** 成员并且已针对 ndis 6.20 更新的结构，其引用页包含 ndis 6.20 和更高版本的驱动程序的新信息。 如果没有针对 NDIS 6.20 的结构的更新，则为 NDIS 6.0 或 NDIS 6.1 驱动程序提供的信息也适用于 NDIS 6.20 和更高版本的驱动程序。

 

 

