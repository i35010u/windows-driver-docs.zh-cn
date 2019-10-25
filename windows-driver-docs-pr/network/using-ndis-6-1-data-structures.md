---
title: 使用 NDIS 6.1 数据结构
description: 使用 NDIS 6.1 数据结构
ms.assetid: 425cd2dc-99b0-4bed-8f7b-c291769c420a
keywords:
- 数据结构 WDK 网络
- NDIS WDK，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2392aee51206faf58a5bec34dc9173a7e56563b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842988"
---
# <a name="using-ndis-61-data-structures"></a>使用 NDIS 6.1 数据结构





NDIS 可支持同一数据结构的多个版本。 在 Windows Server 2008、Windows Vista Service Pack 1 （SP1）或这两个操作系统中使用更新结构的 NDIS 6.1 驱动程序必须在 NDIS\_对象中报告正确的**修订版**成员和**Size**成员值[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)当驱动程序初始化 NDIS 6.1 数据结构时，位于结构的**标头**成员（如果有）的标头结构。

**请注意**  确定正确的版本和大小信息，请参阅每个包含**标头**成员的结构的参考页。 包含**标头**成员并且已针对 ndis 6.1 更新的结构的引用页包含 ndis 6.1 驱动程序的新信息。 如果没有针对 NDIS 6.1 的结构的更新，则为 NDIS 6.0 驱动程序提供的信息也适用于 NDIS 6.1 驱动程序。

 

 

 





