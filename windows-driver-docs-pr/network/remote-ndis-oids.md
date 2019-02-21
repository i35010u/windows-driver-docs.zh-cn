---
title: 远程 NDIS Oid
description: 远程 NDIS Oid
ms.assetid: c97592e8-f395-475e-8e6c-6366d1605075
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd4b9d252b537c96160a390220b8245d8ba92bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526481"
---
# <a name="remote-ndis-oids"></a>远程 NDIS Oid





本部分列出了适用于远程 NDIS 以太网设备必需和可选 NDIS Oid。 列表会考虑的唯一属性的远程 NDIS 设备和远程 NDIS 微型端口驱动程序，因此该列表不是正常的 NDIS 无连接的微型端口驱动程序将支持的列表相同。 某些 Oid 都*设置*并*查询*Oid; 如果必需 OID 定义为这两者，则它必须由远程 NDIS 设备支持，同时[远程\_NDIS\_设置\_MSG](remote-ndis-set-msg.md)并[远程\_NDIS\_查询\_MSG](remote-ndis-query-msg.md)。 有关 Oid 的详细说明，请参阅 Microsoft Windows 驱动程序开发工具包 (DDK)。

远程 NDIS Oid 的以下列表分为两组，常规 OID 和 802.3 特定 OID。 此外，每个组包含的子部分的统计信息 OID 查询。 常规 Oid 所需的任何网络设备。

-   [常规 Oid](general-oids2.md)
-   [常规统计信息 Oid](general-statistic-oids.md)
-   [802.3 Oid](802-3-oids.md)
-   [802.3 统计信息 Oid](802-3-statistic-oids.md)
-   [可选的电源管理 Oid](optional-power-management-oids.md)
-   [Oid 的可选网络唤醒](optional-network-wake-up-oids.md)

 

 





