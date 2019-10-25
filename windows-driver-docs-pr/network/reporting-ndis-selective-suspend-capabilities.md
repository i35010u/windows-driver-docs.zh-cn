---
title: 报告 NDIS 选择性挂起功能
description: 报告 NDIS 选择性挂起功能
ms.assetid: 8A738A51-D116-4DDC-96B7-17D046B6890D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0b07dbfb0e9339dcd93a336f0987f2e896ff9ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842039"
---
# <a name="reporting-ndis-selective-suspend-capabilities"></a>报告 NDIS 选择性挂起功能


从 NDIS 6.30 开始，微型端口驱动程序必须报告驱动程序是否已启用对 NDIS 选择性挂起的支持。 通过 **\*SelectiveSuspend**标准化 INF 关键字的设置启用或禁用对 NDIS 选择性挂起的支持。 有关此 INF 关键字的详细信息，请参阅[用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

当 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，微型端口驱动程序通过执行以下步骤来报告其对 NDIS 选择性挂起支持的支持：

1.  驱动程序使用底层硬件的电源管理功能初始化[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

    如果驱动程序支持 NDIS 选择性挂起，则必须按如下所示将[**ndis\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的成员设置为：

    -   微型端口驱动程序必须指定 NDIS\_PM\_功能\_修订版本\_2，NDIS\_SIZEOF [ **\_\_\_\_NDIS\_PM\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**标头**成员内的功能结构。
    -   如果 **\*SelectiveSuspend**关键字的值为1，则启用对 NDIS 选择性挂起的微型端口驱动程序支持。 微型端口驱动程序通过将 NDIS\_PM 设置\_选择性\_挂起此结构的**Flags**成员内的\_支持标志来报告此情况。

2.  初始化[**ndis\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构后，微型端口驱动程序会将 [**NDIS\_微型端口\_适配器的 PowerManagementCapabilitiesEx 成员设置\_常规\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)指向初始化后的**NDIS\_PM\_功能**结构的属性结构。 当驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)时，微型端口驱动程序将指向**NDIS\_微型\_端口**的指针传递到*MiniportAttributes*参数中的常规\_属性结构\_才能.

微型端口驱动程序用于报告 NDIS 选择性挂起的支持状态的方法基于用于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

 

 





