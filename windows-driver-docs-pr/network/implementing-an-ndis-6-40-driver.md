---
title: 实现 NDIS 6.40 驱动程序
description: NDIS 6.40 驱动程序必须遵循在实现 NDIS 6.30 驱动程序中定义的要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92be066632e5d3b33b93e21c016886235ff04093
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798093"
---
# <a name="implementing-an-ndis-640-driver"></a>实现 NDIS 6.40 驱动程序


NDIS 6.40 驱动程序必须遵循在 [实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中定义的要求。

此外，NDIS 6.40 驱动程序必须符合以下要求：

-   当 ndis 6.40 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。

    必须在 NDIS Xxx 驱动程序特征结构中更新主要和次要 NDIS 版本号 \_ *Xxx* \_ \_ ，才能支持 ndis 6.40。 **MajorNdisVersion** 成员必须包含 **6** 个，并且 **MinorNdisVersion** 成员必须包含 **40**。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息，请参阅 [编译 NDIS 6.40 驱动程序](compiling-an-ndis-6-40-driver.md)。

-   适用于 Windows 8.1 和 Windows Server 2012 R2 操作系统的 NDIS 6.40 微型端口驱动程序必须使用 NDIS 6.40 版本的数据结构。 有关详细信息，请参阅 [使用 NDIS 6.40 数据结构](using-ndis-6-40-data-structures.md)。

 

 





