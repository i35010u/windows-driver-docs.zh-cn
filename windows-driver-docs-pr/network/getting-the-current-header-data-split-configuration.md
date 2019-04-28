---
title: 获取当前的标头数据拆分配置
description: 获取当前的标头数据拆分配置
ms.assetid: 62c5e362-4e19-465d-85a8-a8277cb46f5d
keywords:
- 标头数据拆分 WDK、 配置
- 当前标头数据拆分配置 WDK 网络
- 状态信息 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee8134b50741203f7951ea8417f3d387e5ce480a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349897"
---
# <a name="getting-the-current-header-data-split-configuration"></a>获取当前的标头数据拆分配置





若要获取当前标头数据拆分微型端口适配器，过量驱动程序的设置或用户模式应用程序可以查询[OID\_代\_HD\_拆分\_当前\_配置](https://msdn.microsoft.com/library/windows/hardware/ff569586) OID。 但是，过量驱动程序应使用 NDIS 可用于向其在初始化期间，状态指示的信息。

系统管理员可以使用与 OID 关联的 GUID\_GEN\_HD\_拆分\_当前\_通过 WMI 界面配置 OID。 有关详细信息标头数据拆分 WMI Guid，请参阅[标头数据拆分为 WMI 支持](wmi-support-for-header-data-split.md)。

NDIS 句柄[OID\_代\_HD\_拆分\_当前\_配置](https://msdn.microsoft.com/library/windows/hardware/ff569586)代表微型端口驱动程序。 NDIS 维护当前的标头数据拆分基于微型端口驱动程序初始化属性的配置信息并[ **NDIS\_状态\_HD\_拆分\_当前\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff567370)状态指示。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[ **NDIS\_HD\_拆分\_当前\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff565696)结构。 NDIS 还提供了 NDIS\_HD\_拆分\_当前\_到在初始化过程并通过状态指示过量驱动程序的配置结构。

当微型端口驱动程序收到[OID\_代\_HD\_拆分\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569587)集请求，该驱动程序必须使用的内容[ **NDIS\_HD\_拆分\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565701)结构，以更新当前的微型端口适配器配置。 更新后，微型端口驱动程序必须报告更改，并[ **NDIS\_状态\_HD\_拆分\_当前\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567370)状态指示。 状态指示可确保所有基础驱动程序更新使用新的信息。

当调用 NDIS [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数的 NDIS 6.1 或更高版本协议驱动程序，NDIS 提供[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)用一个指针指向的结构[ **NDIS\_HD\_拆分\_当前\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff565696)结构。

当调用 NDIS [ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905) NDIS 6.1 或更高版本筛选器驱动程序，NDIS 函数提供[ **NDIS\_筛选器\_附加\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)结构的指针到 NDIS\_HD\_拆分\_当前\_配置结构。

 

 





