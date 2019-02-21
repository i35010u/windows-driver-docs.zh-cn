---
title: 实现 6.20 NDIS 驱动程序
description: 实现 6.20 NDIS 驱动程序
ms.assetid: 6c6f83ff-2a6f-4e5d-acc0-70835429312d
keywords:
- NDIS 6.20 WDK，实现一个驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c911117c3c51f89408cfc357e960b78711a564f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521439"
---
# <a name="implementing-an-ndis-620-driver"></a>实现 6.20 NDIS 驱动程序





NDIS 6.20 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。

必须更新的主版本号和次的 NDIS 版本编号在 NDIS\_*Xxx*\_驱动程序\_支持 NDIS 6.20 特征结构。 **MajorNdisVersion**成员必须包含 6 并**MinorNdisVersion**成员必须包含 20。 此要求适用于微型端口、 协议和筛选器驱动程序。 您还必须更新的版本信息对于编译器，请参阅[编译 NDIS 6.20 驱动程序](compiling-an-ndis-6-20-driver.md)。

NDIS 6.20 电源管理服务是强制性的 NDIS 6.20 和更高版本的微型端口驱动程序。 有关 NDIS 6.20 电源管理接口的详细信息，请参阅[NDIS 6.20 电源管理增强功能](power-management-enhancements-in-ndis-6-20.md)。

NDIS 直接 OID 请求接口是必需的 NDIS 6.20 和更高版本的微型端口驱动程序。 有关直接 Oid 接口的详细信息，请参阅[直接 OID 请求接口在 NDIS 6.1](direct-oid-request-interface-in-ndis-6-1.md)。

通知 NDIS 和有关设备的基础驱动程序和驱动程序功能、 NDIS 6.20 和更高版本的驱动程序必须实现以下功能的 NDIS 6.20 设备功能接口：

-   [电源管理](power-management-enhancements-in-ndis-6-20.md)

-   [接收方缩放 (RSS)](ndis-receive-side-scaling2.md)

-   [虚拟机队列 (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)

NDIS 6.20 和更高版本的驱动程序必须支持接收端限制 (RST) 中的接收中断。 RST 的详细信息，请参阅[接收端限制在 NDIS 6.20](receive-side-throttle-in-ndis-6-20.md)。

将为使用已过时接口使用 NDIS 6.20 等效的代码。 有关已过时的函数的详细信息，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。 有关更新结构，以支持 NDIS 6.20 版本信息，请参阅[使用 NDIS 6.20 数据结构](using-ndis-6-20-data-structures.md)。

使用 NDIS 接口支持超过 64 个处理器，例如，使用 NDIS 6.20 读取和写入锁定接口。 有关对超过 64 个处理器的支持的详细信息，请参阅[支持超过 64 个处理器中 NDIS 6.20](support-for-more-than-64-processors-in-ndis-6-20.md)。

 

 





