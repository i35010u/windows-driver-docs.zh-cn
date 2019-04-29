---
title: WMI 的 NDIS 支持
description: WMI 的 NDIS 支持
ms.assetid: ce35ddb4-bf18-4ba1-bc6f-dbe659f5d781
keywords:
- Windows Management Instrumentation WDK 网络
- 微型端口驱动程序 WDK 网络，WMI 支持
- NDIS 微型端口驱动程序 WDK，WMI 支持
- WMI WDK 网络
- 协议驱动程序 WDK 网络，WMI 支持
- NDIS 协议驱动程序 WDK，WMI 支持
- 图标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb5f11c654adf814a47ed669fad989fdaf2bef9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387370"
---
# <a name="ndis-support-for-wmi"></a>WMI 的 NDIS 支持





通过 NDIS，客户端的 Windows Management Instrumentation (WMI) 可以获取和设置的信息，该 NDIS 和 NDIS 驱动程序服务。 WMI 客户端还可以注册以接收状态更新。

NDIS 自动注册为每个 wmi 的微型端口适配器名虚拟连接 (VCs) 和一组的全局唯一标识符 (Guid) 的微型端口适配器。 有关这些 Guid 的详细信息，请参阅[标准微型端口驱动程序 Oid 注册与 WMI](standard-miniport-driver-oids-registered-with-wmi.md)。 微型端口驱动程序也可以提供支持自定义对象标识符 (Oid) 和自定义状态指示，作为[自定义 Oid 和状态指示](customized-oids-and-status-indications.md)主题介绍。

NDIS 不提供 WMI 支持协议驱动程序。 协议驱动程序或中间的驱动程序，可以为自身创建设备对象和直接向 WMI 注册。 有关直接向 WMI 注册的详细信息，请参阅[注册为 WMI 数据提供程序](https://msdn.microsoft.com/library/windows/hardware/ff560870)。

有关 WMI 体系结构的详细信息，请参阅[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139)。

本部分包括：

[注册和注销的与 WMI 的 NDIS 微型端口驱动程序](registration-and-deregistration-of-ndis-miniport-drivers-with-wmi.md)

[映射的 Oid 和微型端口驱动程序状态的 Guid](mapping-of-guids-to-oids-and-miniport-driver-status.md)

[对命名 VCs 的支持](support-for-named-vcs.md)

[NDIS 支持 WMI 操作](ndis-supported-wmi-operations.md)

[标准 WMI Oid 和状态指示](standard-wmi-oids-and-status-indications.md)

[自定义的 Oid 和状态指示](customized-oids-and-status-indications.md)

[NDIS WMI Guid](ndis-wmi-guids.md)

 

 





