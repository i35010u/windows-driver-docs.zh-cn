---
title: 将 NDIS 6.x 驱动程序移植到 NDIS 6.80
description: 对于 NDIS 协议、筛选器和中间驱动程序，NDIS 6.80 与 NDIS 6.60 完全相同。 有关 NDIS 6.80 的新增功能的详细信息，请参阅 NDIS 6.80 简介。
ms.date: 07/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f5ed720adad9cf34c530f120fd2a06f406c74b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786711"
---
# <a name="porting-ndis-6x-drivers-to-ndis-680"></a>将 NDIS 6.x 驱动程序移植到 NDIS 6.80

对于 NDIS 微型端口、协议、筛选器和中间驱动程序，NDIS 6.80 与 NDIS 6.70 完全相同。 对于 NIC 驱动程序，Get-netadapter 类扩展 (NetAdapterCx) 已从 NDIS 6.70 中的1.0 版升级到 NDIS 6.80 中的1.1 版本。 若要将 NDIS 1.x 微型端口驱动程序移植到 NetAdapterCx，请参阅将 [ndis 微型端口驱动程序迁移到 NetAdapterCx](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md)。

有关 NDIS 6.80 的新增功能的详细信息，包括特定于此版本的 NDIS 的实现和编译详细信息，请参阅 [NDIS 6.80 简介](introduction-to-ndis-6-80.md)。

如果要将 NDIS 6. x 微型端口、协议、筛选器或中间驱动程序移植到 NDIS 6.80，应熟悉驱动程序版本与6.80 之间对每个版本的更改。 有关以前的 NDIS 1.x 版本的详细信息，请参阅以下主题：

- [NDIS 6.70 简介](introduction-to-ndis-6-70.md)
- [NDIS 6.60 简介](introduction-to-ndis-6-60.md)
- [NDIS 6.50 简介](introduction-to-ndis-6-50.md)
- [NDIS 6.40 简介](introduction-to-ndis-6-40.md)
- [NDIS 6.30 简介](introduction-to-ndis-6-30.md)
- [NDIS 6.20 简介](introduction-to-ndis-6-20.md)
- [NDIS 6.1 简介](introduction-to-ndis-6-1.md)
- [NDIS 6.0 简介](introduction-to-ndis-6-0.md)

