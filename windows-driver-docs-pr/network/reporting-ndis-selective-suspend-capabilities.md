---
title: 报告 NDIS 选择性挂起功能
description: 报告 NDIS 选择性挂起功能
ms.assetid: 8A738A51-D116-4DDC-96B7-17D046B6890D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef06c17c209901206be6b774281311ef6fbb448
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566493"
---
# <a name="reporting-ndis-selective-suspend-capabilities"></a>报告 NDIS 选择性挂起功能


从 NDIS 6.30 微型端口驱动程序必须报告是否驱动程序已启用支持 NDIS 选择性挂起。 支持的 NDIS 选择性挂起是启用还是禁用的设置通过 **\*SelectiveSuspend**标准化 INF 关键字。 有关此 INF 关键字的详细信息，请参阅[NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

NDIS 时调用的驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，微型端口驱动程序报告其支持的 NDIS 选择性挂起支持通过执行以下步骤：

1.  该驱动程序初始化[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构与基础硬件的电源管理功能。

    如果该驱动程序可以支持 NDIS 选择性挂起，则必须设置的成员[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构，如下所示：

    -   微型端口驱动程序必须指定 NDIS\_PM\_功能\_修订\_2 和 NDIS\_SIZEOF\_NDIS\_PM\_功能\_修订\_修订版本和长度的 2 [ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)内结构的结构**标头**成员。
    -   如果 **\*SelectiveSuspend**关键字的一个值，则启用微型端口驱动程序支持的 NDIS 选择性挂起。 微型端口驱动程序将此报告通过设置 NDIS\_PM\_选择性\_挂起\_内的支持标志**标志**此结构的成员。

2.  已初始化后[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构，微型端口驱动程序集**PowerManagementCapabilitiesEx**成员[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构，以指向已初始化**NDIS\_PM\_功能**结构。 微型端口驱动程序将传递一个指向**NDIS\_微型端口\_适配器\_常规\_特性**结构*MiniportAttributes*当驱动程序调用的参数[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

支持状态的 NDIS 选择性挂起报告的微型端口驱动程序使用的方法基于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

 

 





