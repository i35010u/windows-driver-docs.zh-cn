---
title: 将 NDIS 6.x 驱动程序移植到 NDIS 6.80
description: 对于 NDIS 协议、 筛选和中间驱动程序，NDIS 6.80 大体上是 NDIS 6.60 相同。 NDIS 6.80 的新功能的详细信息，请参阅 NDIS 6.80 简介。
ms.assetid: E5801DCE-B4D8-4BC6-B240-16BD9DB2B1F8
ms.date: 07/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8249bf6c9c4d7840d0560464d5a62017ef291cbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358719"
---
# <a name="porting-ndis-6x-drivers-to-ndis-680"></a>将 NDIS 6.x 驱动程序移植到 NDIS 6.80

对于 NDIS 微型端口、 协议、 筛选和中间驱动程序，NDIS 6.80 大体上是 NDIS 6.70 相同。 NIC 驱动程序，请 NetAdapter 类扩展 (NetAdapterCx) 已更新到版本 1.0 中 NDIS 6.70 NDIS 6.80 的 1.1 版。 若要移植到 NetAdapterCx NDIS 6.x 微型端口驱动程序，请参阅[NetAdapterCx 移植 NDIS 微型端口驱动程序](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md)。

有关 NDIS 6.80 的新功能的详细信息，包括实现和编译的详细信息特定于此版本的 NDIS，请参阅[简介 NDIS 6.80](introduction-to-ndis-6-80.md)。

如果要将迁移的 NDIS 6.x 微型端口、 协议、 筛选器或到 NDIS 6.80 中间驱动程序，您应熟悉对您的驱动程序版本和 6.80 之间每个版本所做的更改。 有关以前 NDIS 6.x 版本的详细信息，请参阅以下主题：

- [NDIS 6.70 简介](introduction-to-ndis-6-70.md)
- [NDIS 6.60 简介](introduction-to-ndis-6-60.md)
- [NDIS 6.50 简介](introduction-to-ndis-6-50.md)
- [NDIS 6.40 简介](introduction-to-ndis-6-40.md)
- [NDIS 6.30 简介](introduction-to-ndis-6-30.md)
- [NDIS 6.20 简介](introduction-to-ndis-6-20.md)
- [NDIS 6.1 简介](introduction-to-ndis-6-1.md)
- [NDIS 6.0 简介](introduction-to-ndis-6-0.md)

