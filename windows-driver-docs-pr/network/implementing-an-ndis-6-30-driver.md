---
title: 实现 NDIS 6.30 驱动程序
description: 实现 NDIS 6.30 驱动程序
ms.assetid: B1B48ED9-10F1-45F2-AA7C-270B637B5A36
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d34c941d4e2db744e01fc54965591ac0912350e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563295"
---
# <a name="implementing-an-ndis-630-driver"></a>实现 NDIS 6.30 驱动程序


NDIS 6.30 驱动程序必须遵循在中定义的要求[实现 NDIS 6.20 驱动程序](implementing-an-ndis-6-20-driver.md)。

此外，NDIS 6.30 驱动程序必须符合以下要求：

-   NDIS 6.30 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。

    必须更新的主版本号和次的 NDIS 版本编号在 NDIS\_*Xxx*\_驱动程序\_支持 NDIS 6.30 特征结构。 **MajorNdisVersion**成员必须包含**6**并**MinorNdisVersion**成员必须包含**30**。 此要求适用于微型端口、 协议和筛选器驱动程序。 您还必须更新的版本信息对于编译器，请参阅[编译 NDIS 6.30 驱动程序](compiling-an-ndis-6-30-driver.md)。

-   若要告知设备和驱动程序功能，NDIS 6.30 NDIS 和基础驱动程序驱动程序必须实现以下功能的 NDIS 6.30 设备功能接口：

    -   [虚拟化网络](virtualized-networking-enhancements-in-ndis-6-30.md)

    -   [电源管理](power-management-enhancements-in-ndis-6-30.md)

    -   [NDIS 服务质量 (QoS)](quality-of-service--qos--support-in-ndis-6-30.md)

-   为 Windows 8 和 Windows Server 2012 操作系统的 NDIS 6.30 微型端口驱动程序必须使用数据结构的 NDIS 6.30 版本。 有关详细信息，请参阅[使用 NDIS 6.30 数据结构](using-ndis-6-30-data-structures.md)。

 

 





