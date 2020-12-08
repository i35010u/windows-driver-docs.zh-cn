---
title: 实现 NDIS 6.30 驱动程序
description: 实现 NDIS 6.30 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45260a27bd9c7cfbf0edd76dc3f5102690357a2e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802359"
---
# <a name="implementing-an-ndis-630-driver"></a>实现 NDIS 6.30 驱动程序


NDIS 6.30 驱动程序必须遵循在 [实现 NDIS 6.20 驱动程序](implementing-an-ndis-6-20-driver.md)中定义的要求。

此外，NDIS 6.30 驱动程序必须符合以下要求：

-   当 ndis 6.30 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。

    必须在 NDIS Xxx 驱动程序特征结构中更新主要和次要 NDIS 版本号 \_ *Xxx* \_ \_ ，才能支持 ndis 6.30。 **MajorNdisVersion** 成员必须包含 **6** 个，并且 **MinorNdisVersion** 成员必须包含 **30** 个。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息，请参阅 [编译 NDIS 6.30 驱动程序](compiling-an-ndis-6-30-driver.md)。

-   为了向 NDIS 和过量驱动程序提供有关设备和驱动程序功能的信息，NDIS 6.30 驱动程序必须为以下功能实现 NDIS 6.30 设备功能接口：

    -   [虚拟化网络](virtualized-networking-enhancements-in-ndis-6-30.md)

    -   [电源管理](power-management-enhancements-in-ndis-6-30.md)

    -   [NDIS 服务质量 (QoS) ](quality-of-service--qos--support-in-ndis-6-30.md)

-   适用于 Windows 8 和 Windows Server 2012 操作系统的 NDIS 6.30 微型端口驱动程序必须使用 NDIS 6.30 版本的数据结构。 有关详细信息，请参阅 [使用 NDIS 6.30 数据结构](using-ndis-6-30-data-structures.md)。

 

 





