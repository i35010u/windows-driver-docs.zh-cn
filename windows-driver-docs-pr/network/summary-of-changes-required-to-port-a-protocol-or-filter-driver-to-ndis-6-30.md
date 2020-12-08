---
title: 到 NDIS 6.3 的端口协议或筛选器驱动程序的更改摘要
description: 若要更新 NDIS 1.x 协议或筛选器驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f66f7bc24d99438dbcc82bf52858633c2d497ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825411"
---
# <a name="summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-630"></a>将协议或筛选器驱动程序移植到 NDIS 6.30 所要做出的更改摘要


若要更新 NDIS 1.x 协议或筛选器驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。

-   [生成环境](#build-environment)
-   [协议驱动程序的常规移植要求](#general-porting-requirements-for-protocol-drivers)
-   [筛选器驱动程序的常规移植要求](#general-porting-requirements-for-filter-drivers)

## <a name="build-environment"></a>生成环境


-   将预处理器定义 NDIS60 或 NDIS61 或 NDIS620 （如果存在）替换为 NDIS630。
-   \_*Xxx* \_ \_ 如 [实现 ndis 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中所述，在 ndis Xxx 驱动程序特征结构中更新主要和次要的 ndis 版本号。

## <a name="general-porting-requirements-for-protocol-drivers"></a>协议驱动程序的常规移植要求


协议驱动程序应始终完成 **NetEventSetPower** ，而无需等待数据包。 有关详细信息，请参阅：

-   [NDIS 6.30 中的电源管理增强](power-management-enhancements-in-ndis-6-30.md)
-   [处理协议驱动程序中的 PnP 事件和电源管理事件](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)

有关 NDIS 6.30 功能的详细信息，请参阅 [ndis 6.30 简介](introduction-to-ndis-6-30.md)。

## <a name="general-porting-requirements-for-filter-drivers"></a>筛选器驱动程序的常规移植要求


筛选器驱动程序应始终完成 **NetEventSetPower** ，而无需等待数据包。 有关详细信息，请参阅：

-   [NDIS 6.30 中的电源管理增强](power-management-enhancements-in-ndis-6-30.md)
-   [**NDIS \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)
-   [**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)
-   [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md)

有关 NDIS 6.30 功能的详细信息，请参阅 [ndis 6.30 简介](introduction-to-ndis-6-30.md)。

 

