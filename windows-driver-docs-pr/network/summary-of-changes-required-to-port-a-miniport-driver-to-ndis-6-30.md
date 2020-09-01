---
title: 将微型端口驱动程序移植到 NDIS 6.30 的更改摘要
description: 若要更新 NDIS 1.x 微型端口驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。
ms.assetid: 1EA926FE-367E-4A63-A197-60137D679AE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 467fbc0442b89c51d8dce145981bc89cea06c8d5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214312"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-630"></a>将微型端口驱动程序移植到 NDIS 6.30 所要做出的更改摘要


若要更新 NDIS 1.x 微型端口驱动程序以支持 NDIS 6.30，必须按照以下各节中所述修改它。

-   [生成环境和测试](#build-environment-and-testing)
-   [一般移植要求](#general-porting-requirements)
-   [Wi-fi Direct 微型端口驱动程序](#wi-fi-direct-miniport-drivers)
-   [基于 USB 的 WWAN (移动宽带) 微型端口驱动程序](#usb-based-wwan-mobile-broadband-miniport-drivers)

有关 NDIS 6.30 功能的详细信息，请参阅 [ndis 6.30 简介](introduction-to-ndis-6-30.md)。

## <a name="build-environment-and-testing"></a>生成环境和测试


-   将预处理器定义 NDIS60 \_ 微型端口或 NDIS61 \_ 微型端口或 NDIS620 微型端口替换 \_ 为 NDIS630 \_ 微型端口。 有关详细信息，请参阅 [编译 NDIS 6.30 驱动程序](compiling-an-ndis-6-30-driver.md)
-   将预处理器定义 NDIS60 或 NDIS61 或 NDIS620 （如果存在）替换为 NDIS630。
    **注意**   此项仅适用于 NDIS 中间、协议和筛选器驱动程序。 大多数 NDIS 微型端口驱动程序不需要此预处理器定义。

     

-   在 NDIS 6.30 中，如果有两个适配器同时插入系统或系统启动期间，NDIS 就可以并行调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 两次。 请确保在此 "并行启动" 条件下测试微型端口驱动程序。

## <a name="general-porting-requirements"></a>一般移植要求


-   \_*Xxx* \_ \_ 如[实现 ndis 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中所述，在 ndis Xxx 驱动程序特征结构中更新主要和次要的 ndis 版本号。
-   对于所有已针对 NDIS 6.30 更新的结构，微型端口驱动程序需要更新结构的 **标头** 成员以及正确的 **版本** 和 **大小** 值。 有关详细信息，请参阅 [使用 NDIS 6.30 数据结构](using-ndis-6-30-data-structures.md)。
-   所有微型端口驱动程序都应实现不暂停挂起功能。 有关详细信息，请参阅：
    -   [NDIS 6.30 中的电源管理增强](power-management-enhancements-in-ndis-6-30.md)
    -   [**NDIS \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)
    -   [**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)
    -   [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md)

## <a name="wi-fi-direct-miniport-drivers"></a>Wi-fi Direct 微型端口驱动程序


在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)期间，wi-fi Direct 功能的微型端口驱动程序必须初始化默认的 802.11 MAC 实体。 它还必须使用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数报告其 wi-fi Direct 和虚拟 wi-fi 功能。

**注意**   不需要驱动程序向 NDIS 注册与默认 MAC 实体对应的 NDIS 端口。

 

## <a name="usb-based-wwan-mobile-broadband-miniport-drivers"></a>基于 USB 的 WWAN (移动宽带) 微型端口驱动程序


对于基于 USB 的移动宽带设备，Windows 8 提供了一个适用于符合 MBIM 规范的设备的类驱动程序。 此模型称为移动宽带 (MB) 类驱动程序。 但是，类驱动程序无法支持 MB 设备公开的所有功能。 出于此原因，MB 功能提供了定义完善的机制，可用于扩展类驱动程序功能。 有关详细信息，请参阅 [MB 设备服务](mb-device-services.md)。

如果基于 USB 的 WWAN 微型端口驱动程序无法实现 MB 类驱动程序，则必须至少实现 [NDIS 选择性挂起](ndis-selective-suspend.md) 功能。

 

