---
title: 设置当前的标头数据拆分配置
description: 设置当前的标头数据拆分配置
ms.assetid: b5b20ce8-1522-4729-8d0a-bc2d2c5afff2
keywords:
- 标头数据拆分 WDK、 配置
- 当前标头数据拆分配置 WDK 网络
- 状态信息 WDK 标头数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13c7b9060bdb950f2036363a83f4c3ace7fecd49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346641"
---
# <a name="setting-the-current-header-data-split-configuration"></a>设置当前的标头数据拆分配置





NDIS 和基础驱动程序或用户模式应用程序使用[OID\_代\_HD\_拆分\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569587)OID，设置当前标头数据拆分微型端口适配器的设置。 NDIS 6.1 和更高版本的微型端口驱动程序提供标头数据拆分服务必须支持此 OID。 否则，此 OID 是可选的。

系统管理员可以使用与此 OID 通过 WMI 接口相关联的 GUID。 有关详细信息标头数据拆分 WMI Guid，请参阅[标头数据拆分为 WMI 支持](wmi-support-for-header-data-split.md)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含[ **NDIS\_HD\_拆分\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565701)结构。

如果 NDIS\_HD\_拆分\_合并\_所有\_标头标志中**HDSplitCombineFlags**成员 NDIS\_HD\_拆分\_设置参数，微型端口适配器必须将所有拆分帧结合都起来。 如果硬件中启用了标头数据拆分，微型端口驱动程序必须先组合的标头和数据之前，驱动程序指示到 NDIS 帧。

例如，NDIS 可能使用 OID\_GEN\_HD\_拆分\_参数 OID 以设置 NDIS\_HD\_拆分\_合并\_所有\_标头中的标记时 NDIS 5。*x*协议驱动程序将绑定到 NDIS 6.1 微型端口适配器。 NDIS 之前它将 OID 传递给微型端口驱动程序和更新的微型端口适配器处理此 OID  **\*HeaderDataSplit**关键字，如果需要进行标准化。 如果禁用了标头数据拆分，则 NDIS 不向微型端口适配器发送此 OID。

 

 





