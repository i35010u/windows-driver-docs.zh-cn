---
title: NDIS 管理信息和 OID
description: NDIS 管理信息和 OID
ms.assetid: 5737634e-ee80-44d4-9dc8-c2ef97670809
keywords:
- WMI WDK 网络，管理信息库
- 管理信息基本 WDK 网络
- 动态配置信息 WDK 网络
- 统计信息 WDK 网络
- 管理信息基本 WDK 网络，对象
- Mib WDK 网络
- 对象标识符 WDK 网络
- Oid WDK 网络，管理信息库
- 操作特征 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c16649ff6499118b1f18310fc43cc5e765186496
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842385"
---
# <a name="ndis-management-information-and-oids"></a>NDIS 管理信息和 OID





每个微型端口驱动程序都包含自己的*管理信息基础（MIB）* ，这是一个信息块，驱动程序将在其中存储管理实体可以查询或设置的动态配置信息和统计信息。 "以太网多播地址列表" 是配置信息的示例。 收到的广播数据包的数目是统计信息的示例。 MIB 中的每个信息元素称为*对象*。 为了引用每个此类托管对象，NDIS 定义了一个*对象标识符（OID）* 。 因此，如果管理实体要查询或设置特定的托管对象，则必须为该对象提供特定 OID。

MIB 跟踪三类对象：

-   所有 NDIS 微型端口驱动程序的常规对象。

-   特定于给定媒体类型（如以太网）的所有 NDIS 小型端口驱动程序的对象。

-   特定于特定供应商实现的对象。

WDK 文档的 "网络参考" 部分介绍了*一般*和必需的*特定媒体*oid。 特定网络接口卡（NIC）驱动程序的特定于实现的 Oid 应在附带的微型端口驱动程序随附的文档中列出和说明。

对象归类为*操作特性*（例如，多播地址列表）或*统计信息*（例如，已接收的广播数据包），并且它们也归类为*必需*或*可选*。 常规或特定于媒体的类的所有操作特征对象都是必需的，但只有部分统计信息对象是必需的。 所有特定于实现的对象归类为强制。

有关 OID 分类的详细信息，请参阅[NDIS oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 





