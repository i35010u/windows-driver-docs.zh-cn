---
title: 到 NDIS 6.3 的端口协议或筛选器驱动程序的更改摘要
description: 若要更新 NDIS 1.x 协议或筛选器驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。
ms.assetid: 1C6CB2E1-C129-4F3B-AF7D-357580BEE7F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1f75ecb622a6374d28a002b3bfb7f1fa2335920
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841804"
---
# <a name="summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-630"></a>将协议或筛选器驱动程序移植到 NDIS 6.30 所要做出的更改摘要


若要更新 NDIS 1.x 协议或筛选器驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。

-   [生成环境](#build-environment)
-   [协议驱动程序的常规移植要求](#general-porting-requirements-for-protocol-drivers)
-   [筛选器驱动程序的常规移植要求](#general-porting-requirements-for-filter-drivers)

## <a name="build-environment"></a>生成环境


-   将预处理器定义 NDIS60 或 NDIS61 或 NDIS620 （如果存在）替换为 NDIS630。
-   如[实现 ndis 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中所述，在 NDIS\_*XXX*\_驱动程序\_特征结构中更新主要和次要 NDIS 版本号。

## <a name="general-porting-requirements-for-protocol-drivers"></a>协议驱动程序的常规移植要求


协议驱动程序应始终完成**NetEventSetPower** ，而无需等待数据包。 有关详细信息，请参阅：

-   [NDIS 6.30 中的电源管理增强功能](power-management-enhancements-in-ndis-6-30.md)
-   [处理协议驱动程序中的 PnP 事件和电源管理事件](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)

有关 NDIS 6.30 功能的详细信息，请参阅[ndis 6.30 简介](introduction-to-ndis-6-30.md)。

## <a name="general-porting-requirements-for-filter-drivers"></a>筛选器驱动程序的常规移植要求


筛选器驱动程序应始终完成**NetEventSetPower** ，而无需等待数据包。 有关详细信息，请参阅：

-   [NDIS 6.30 中的电源管理增强功能](power-management-enhancements-in-ndis-6-30.md)
-   [ **\_适配器\_注册\_特性的 NDIS\_微型端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)
-   [**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)
-   [OID\_PNP\_集\_电源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

有关 NDIS 6.30 功能的详细信息，请参阅[ndis 6.30 简介](introduction-to-ndis-6-30.md)。

 

 





