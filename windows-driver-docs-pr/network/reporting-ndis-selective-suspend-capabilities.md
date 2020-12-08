---
title: 报告 NDIS 选择性挂起功能
description: 报告 NDIS 选择性挂起功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c3a38627a6e872037c93a720dab052b69776f2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815897"
---
# <a name="reporting-ndis-selective-suspend-capabilities"></a>报告 NDIS 选择性挂起功能


从 NDIS 6.30 开始，微型端口驱动程序必须报告驱动程序是否已启用对 NDIS 选择性挂起的支持。 通过 **\* SELECTIVESUSPEND** 标准化 INF 关键字的设置启用或禁用对 NDIS 选择性挂起的支持。 有关此 INF 关键字的详细信息，请参阅 [用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

当 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，微型端口驱动程序通过执行以下步骤来报告其对 NDIS 选择性挂起支持的支持：

1.  驱动程序使用基础硬件的电源管理功能初始化 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities) 结构。

    如果驱动程序支持对 NDIS 选择性挂起的支持，则必须按如下所示设置 [**ndis \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities) 结构的成员：

    -   微型端口驱动程序必须 \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ 为结构的 **标头** 成员内的 [**ndis \_ pm \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构指定 ndis pm 功能修订版本2和 ndis SIZEOF ndis pm 功能修订版本2。
    -   如果 **\* SelectiveSuspend** 关键字的值为1，则启用对 NDIS 选择性挂起的微型端口驱动程序支持。 微型端口驱动程序通过在 \_ \_ \_ \_ 此结构的 **Flags** 成员内设置 NDIS PM 选择性挂起支持标志来报告这种情况。

2.  初始化 [**ndis \_ pm \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构后，微型端口驱动程序会将 [**Ndis \_ 微型端口 \_ 适配器 \_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的 **PowerManagementCapabilitiesEx** 成员设置为指向已初始化的 **NDIS \_ pm \_ 功能** 结构。 当驱动程序调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数时，微型端口驱动程序将指针传递到 *MiniportAttributes* 参数中的 **NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性** 结构。

微型端口驱动程序用于报告 NDIS 选择性挂起的支持状态的方法基于用于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅 [报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅 [初始化微型端口适配器](initializing-a-miniport-adapter.md)。

 

