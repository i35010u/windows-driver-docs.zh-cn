---
title: NDIS 管理信息和 OID
description: NDIS 管理信息和 OID
ms.assetid: 5737634e-ee80-44d4-9dc8-c2ef97670809
keywords:
- 网络、 管理信息基础 WMI WDK
- 管理信息基本 WDK 网络
- 动态配置信息 WDK 网络
- 统计信息 WDK 网络
- 管理信息基本 WDK 网络对象
- Mib WDK 网络
- 对象标识符 WDK 网络
- Oid WDK 网络管理信息基础
- 操作特征 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3223589498f2a38180af1f00541dd4911268434
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385750"
---
# <a name="ndis-management-information-and-oids"></a>NDIS 管理信息和 OID





每个微型端口驱动程序包含其自身*管理信息基础 (MIB)* ，这是信息块中的驱动程序将动态配置信息和管理实体可以查询的统计信息存储或设置。 以太网多播的地址列表是配置信息的示例。 接收广播数据包数为统计信息的示例。 MIB 中的每个信息元素称为*对象*。 若要引用此类每个托管对象，NDIS 定义*对象标识符 (OID)* 。 因此，如果管理实体想要查询或设置特定的托管的对象，它必须为该对象提供特定的 OID。

MIB 跟踪对象的三个的类：

-   通用的所有 NDIS 微型端口驱动程序的对象。

-   特定于给定媒体的所有 NDIS 微型端口驱动程序的对象类型，例如以太网。

-   特定于特定供应商实现的对象。

*常规*并且是强制性*媒体特定*Oid 都记录在 WDK 文档中的网络参考部分中。 应列出和中给定的微型端口驱动程序附带的文档所述的特定网络接口卡 (NIC) 驱动程序的特定于实现的 Oid。

对象被分类为*运作特点*（例如，多播的地址列表） 或*统计信息*（例如，广播接收的数据包），并且它们也被归类为*必需*或*可选*。 为常规或特定于媒体的类是必需的但只有某些统计信息对象都是必需的所有操作特征对象。 所有特定于实现的对象被分类为必需。

有关 OID 分类的详细信息，请参阅[NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

 

 





