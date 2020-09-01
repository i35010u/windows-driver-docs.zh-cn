---
title: 实现 NDIS 6.20 驱动程序
description: 实现 NDIS 6.20 驱动程序
ms.assetid: 6c6f83ff-2a6f-4e5d-acc0-70835429312d
keywords:
- NDIS 6.20 WDK，实现驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6af50ad24429c2c90fd5cf48d1afccef8524e29f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206443"
---
# <a name="implementing-an-ndis-620-driver"></a>实现 NDIS 6.20 驱动程序





当 ndis 6.20 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。

必须在 NDIS Xxx 驱动程序特征结构中更新主要和次要 NDIS 版本号 \_ *Xxx* \_ \_ ，才能支持 ndis 6.20。 **MajorNdisVersion**成员必须包含6个，并且**MinorNdisVersion**成员必须包含20个。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息，请参阅 [编译 NDIS 6.20 驱动程序](compiling-an-ndis-6-20-driver.md)。

对于 NDIS 6.20 和更高版本的微型端口驱动程序，NDIS 6.20 电源管理服务是必需的。 有关 NDIS 6.20 电源管理接口的详细信息，请参阅 [ndis 6.20 中的电源管理增强功能](power-management-enhancements-in-ndis-6-20.md)。

对于 NDIS 6.20 和更高的微型端口驱动程序，NDIS 直接 OID 请求接口是必需的。 有关直接 Oid 接口的详细信息，请参阅 [NDIS 6.1 中的直接 Oid 请求接口](direct-oid-request-interface-in-ndis-6-1.md)。

若要向 NDIS 和过量驱动程序通知有关设备和驱动程序功能的信息，NDIS 6.20 和更高版本的驱动程序必须为以下功能实现 NDIS 6.20 设备功能接口：

-   [电源管理](power-management-enhancements-in-ndis-6-20.md)

-   [接收方伸缩 (RSS)](./receive-side-scaling-version-2-rssv2-.md)

-   [虚拟机队列 (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)

NDIS 6.20 和更高版本的驱动程序必须支持接收方限制 (RST) 接收中断。 有关 RST 的详细信息，请参阅 [NDIS 6.20 中的接收方限制](receive-side-throttle-in-ndis-6-20.md)。

将使用过时接口的代码替换为 NDIS 6.20 等效项。 有关过时函数的详细信息，请参阅 [NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。 有关更新结构以支持 NDIS 6.20 版本的信息，请参阅 [使用 ndis 6.20 数据结构](using-ndis-6-20-data-structures.md)。

使用支持超过64个处理器的 NDIS 接口，例如，使用 NDIS 6.20 读取和写入锁定接口。 有关对超过64个处理器的支持的详细信息，请参阅 [NDIS 6.20 中对超过64个处理器的支持](support-for-more-than-64-processors-in-ndis-6-20.md)。

 

