---
title: MB 接口概述
description: MB 接口概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0cb1344433aba63ebaddc3cff9e6fa8be056cf8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840643"
---
# <a name="mb-interface-overview"></a>MB 接口概述


本文档介绍移动宽带 (MB) 驱动程序模型。 MB 驱动程序模型是随 Windows 7 和更高版本的 Windows 一起提供的软件体系结构。 它为一组集成的网络功能提供一个框架，该框架基于基于 CDMA 的 (1xRTT/1xEV/1xEV-DO RevA/1xEvDO RevB) 和基于 GSM 的 (GPRS/EDGE/UMTS/HSDPA/TD-SCDMA) 手机技术。

Windows 8 MB 微型端口驱动程序基于 [NDIS 6.30](introduction-to-ndis-6-30.md) 接口。 Windows 7 MB 微型端口驱动程序基于 [NDIS 6.20](introduction-to-ndis-6-20.md) 接口。 MB 微型端口驱动程序必须遵循本文档中所述的 "NDIS 1.x 规范" 相应的 "NDIS 1.x 规范" (DDIs) 。

下图显示了 MB 驱动程序模型的体系结构。

![说明移动宽带驱动程序模型的体系结构的示意图](images/wwanarchitecture.png)

### <a name="terminology"></a>术语

请注意，在整个文档中，将 *无线广域网* (WWAN) 和 *移动宽带* (MB) 用于表示移动宽带技术。

本文档中的 " *激活* " 和 " *激活* " 一词具有两种不同的含义。 *激活* 期限与服务激活相关，例如，当网络提供商必须在使用提供程序的服务之前显式启用 MB 订阅。 术语 *激活* 特定于在基于 GSM 的 (GPRS/EDGE/UMTS/HSDPA/TD-SCDMA) 技术中设置连接。 例如， *pdp 上下文激活* 是指根据 PDP 上下文中指定的参数设置 MB 连接。

*Sim 访问* 是指 (SIM （也称为 R-UIM) ）访问订阅服务器标识模块。 如果 MB 设备没有 SIM/R-UIM 作为物理实体，而是在设备中有一个逻辑等效项，则此术语同样适用于该逻辑环路。 当不需要使用 SIM 时，无需使用微型端口驱动程序即可从 SIM 中检索信息以完成请求。

### <a name="semantics"></a>语义

在用户模式下，MB 服务组件不能在内核模式下直接与具有 MB 微型端口驱动程序的数据交换。 需要媒介（如 WMI 或 [NDIS 筛选器驱动程序](./roadmap-for-developing-ndis-filter-drivers.md) ）。 为简单起见，本文档中未明确讨论这些中介。 但是，这种省略并不意味着 MB 服务和 MB 微型端口驱动程序可以进行直接的数据交换。

以下主题提供了 NDIS 6.20 和 MB OID 语义的摘要，以及微型端口驱动程序执行同步和异步操作时必须遵循的过程，并概述了移动宽带驱动程序模型支持的操作：

[MB/NDIS 6.20 接口概述](mb---ndis-6-20-interfacing-overview.md)

[MB 数据模型](mb-data-model.md)

[MB 操作语义](mb-operational-semantics.md)

[MB 驱动程序模型版本控制](mb-driver-model-versioning.md)

[MB 微型端口驱动程序 INF 要求](mb-miniport-driver-inf-requirements.md)

[MB 微型端口驱动程序类型](mb-miniport-driver-types.md)

[MB 适配器常规属性要求](mb-adapter-general-attribute-requirements.md)

[MB 原始 IP 数据包处理支持](mb-raw-ip-packet-processing-support.md)

[有关 MB 微型端口驱动程序 IP 地址通知的指导原则](guidelines-for-mb-miniport-driver-ip-address-notifications.md)

[MB 微型端口驱动程序错误日志记录](mb-miniport-driver-error-logging.md)

[MB 微型端口驱动程序性能要求](mb-miniport-driver-performance-requirements.md)

 

