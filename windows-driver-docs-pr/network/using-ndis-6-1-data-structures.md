---
title: 使用 NDIS 6.1 数据结构
description: 使用 NDIS 6.1 数据结构
keywords:
- 数据结构 WDK 网络
- NDIS WDK，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b1fd5382a19228b62cce50b05e03132c0092124
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247899"
---
# <a name="using-ndis-61-data-structures"></a>使用 NDIS 6.1 数据结构





NDIS 可支持同一数据结构的多个版本。 当驱动程序初始化 NDIS 6.1 数据结构时，使用 Windows Server 2008、Windows Vista Service Pack 1 (SP1) 或这两种操作系统中的已更新结构的 NDIS 6.1 驱动程序必须在结构的 **标头** 成员（如果有）中报告 [**正确的 \_ \_**](/windows-hardware/drivers/ddi/objectheader/ns-objectheader-ndis_object_header) **修订版** 成员和 **Size** 成员值。

**注意**  若要确定正确的版本和大小信息，请参阅每个包含 **标头** 成员的结构的参考页。 包含 **标头** 成员并且已针对 ndis 6.1 更新的结构的引用页包含 ndis 6.1 驱动程序的新信息。 如果没有针对 NDIS 6.1 的结构的更新，则为 NDIS 6.0 驱动程序提供的信息也适用于 NDIS 6.1 驱动程序。

 

 

