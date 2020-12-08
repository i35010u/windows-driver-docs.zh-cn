---
title: WMI 的 NDIS 支持
description: WMI 的 NDIS 支持
keywords:
- Windows Management Instrumentation WDK 网络
- 微型端口驱动程序 WDK 网络，WMI 支持
- NDIS 微型端口驱动程序 WDK，WMI 支持
- WMI WDK 网络
- 协议驱动程序 WDK 网络，WMI 支持
- NDIS 协议驱动程序 WDK，WMI 支持
- i
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d9b5f24651adc5297da75e753e0f28137b27af9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812995"
---
# <a name="ndis-support-for-wmi"></a>WMI 的 NDIS 支持





通过 NDIS，Windows Management Instrumentation (WMI) 的客户端可以获取和设置 NDIS 和 NDIS 驱动程序服务的信息。 WMI 客户端还可以注册以接收状态更新。

NDIS 自动注册微型端口适配器， (VCs) 命名为虚拟连接，并为每个带 WMI 的微型端口适配器 (Guid) 提供一组全局唯一标识符。 有关这些 Guid 的详细信息，请参阅 [在 WMI 中注册的标准微型端口驱动程序 oid](standard-miniport-driver-oids-registered-with-wmi.md)。 小型端口驱动程序还可以提供对自定义的对象标识符 (Oid) 和自定义状态指示的支持，如 [自定义 oid 和状态指示](customized-oids-and-status-indications.md) 主题所述。

NDIS 不提供对协议驱动程序的 WMI 支持。 协议驱动程序或中间驱动程序可以为自身创建设备对象，并直接使用 WMI 进行注册。 有关使用 WMI 直接注册的详细信息，请参阅 [注册为 Wmi 数据提供程序](../kernel/registering-as-a-wmi-data-provider.md)。

有关 WMI 体系结构的详细信息，请参阅 [Windows Management Instrumentation](../kernel/implementing-wmi.md)。

本节包括：

[在 WMI 中注册和取消注册 NDIS 微型端口驱动程序](registration-and-deregistration-of-ndis-miniport-drivers-with-wmi.md)

[将 GUID 映射到 OID 和微型端口驱动程序状态](mapping-of-guids-to-oids-and-miniport-driver-status.md)

[命名 VC 的支持](support-for-named-vcs.md)

[NDIS 支持的 WMI 操作](ndis-supported-wmi-operations.md)

[标准 WMI OID 和状态指示](standard-miniport-driver-oids-registered-with-wmi.md)

[自定义的 OID 和状态指示](customized-oids-and-status-indications.md)

[NDIS WMI GUID](guid-ndis-status-link-state.md)

 

