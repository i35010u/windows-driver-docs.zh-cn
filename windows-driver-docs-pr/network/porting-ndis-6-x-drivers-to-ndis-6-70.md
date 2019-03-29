---
title: 将 NDIS 6.x 驱动程序移植到 NDIS 6.70
description: 对于 NDIS 协议、 筛选和中间驱动程序，NDIS 6.70 大体上是 NDIS 6.60 相同。 NDIS 6.70 的新功能的详细信息，请参阅 NDIS 6.70 简介。
ms.assetid: DB099908-E8EF-4D4B-95FF-9B17702D4A7B
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: c74de40f4342fcb78996074d470175c27d813fd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575444"
---
# <a name="porting-ndis-6x-drivers-to-ndis-670"></a>将 NDIS 6.x 驱动程序移植到 NDIS 6.70

对于 NDIS 微型端口、 协议、 筛选和中间驱动程序，NDIS 6.70 大体上是 NDIS 6.60 相同。 从 NDIS 6.70，但是，NDIS 驱动程序开发人员还可以编写使用新的网络适配器 WDF 类扩展，也称为 NIC 驱动程序 [NetAdapterCx](../netcx/index.md)。 若要移植到 NetAdapterCx NDIS 6.x 微型端口驱动程序，请参阅[NetAdapterCx 移植 NDIS 微型端口驱动程序](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md)。

有关 NDIS 6.70 的新功能的详细信息，包括实现和编译的详细信息特定于此版本的 NDIS，请参阅[简介 NDIS 6.70](introduction-to-ndis-6-70.md)。

如果要将迁移的 NDIS 6.x 微型端口、 协议、 筛选器或到 NDIS 6.70 中间驱动程序，您应熟悉对您的驱动程序版本和 6.70 之间每个版本所做的更改。 有关以前 NDIS 6.x 版本的详细信息，请参阅以下主题：

- [NDIS 6.60 简介](introduction-to-ndis-6-60.md)
- [NDIS 6.50 简介](introduction-to-ndis-6-50.md)
- [NDIS 6.40 简介](introduction-to-ndis-6-40.md)
- [NDIS 6.30 简介](introduction-to-ndis-6-30.md)
- [NDIS 6.20 简介](introduction-to-ndis-6-20.md)
- [NDIS 6.1 简介](introduction-to-ndis-6-1.md)
- [NDIS 6.0 简介](introduction-to-ndis-6-0.md)

