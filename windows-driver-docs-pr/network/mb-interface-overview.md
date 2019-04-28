---
title: MB 接口概述
description: MB 接口概述
ms.assetid: fcb79029-4225-4759-a130-6ef8b3f2d25d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b71c30c87057ae7544f0170288948ca92ba831
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343387"
---
# <a name="mb-interface-overview"></a>MB 接口概述


本文档说明移动宽带 (MB) 驱动程序模型。 MB 驱动程序模型是使用 Windows 7 和更高版本的 Windows 提供的软件体系结构。 它提供一组集成的网络功能基于 CDMA 基于 （1xRTT/1xEV-不要/1xEV-不要 RevA/1xEvDO RevB） 和基于 GSM 的 (GPRS/边缘/UMTS/HSDPA/t D-SCDMA) 移动电话技术框架。

Windows 8 MB 微型端口驱动程序基于[NDIS 6.30](introduction-to-ndis-6-30.md)接口。 Windows 7 MB 微型端口驱动程序基于[NDIS 6.20](introduction-to-ndis-6-20.md)接口。 MB 微型端口驱动程序必须遵循相应"NDIS 6.x 规范"除了在本文档中所述的设备驱动程序接口 (DDIs)。

下图表示 MB 驱动程序模型的体系结构。

![说明的移动宽带的驱动程序模型的体系结构的关系图](images/wwanarchitecture.png)

### <a name="terminology"></a>术语

请注意，术语*无线广域网*(WWAN) 和*移动宽带*(MB) 可以互换在本文档中来表示移动宽带技术。

条款*激活*并*激活*本文档中具有两个不同的含义。 术语*激活*与服务激活，例如当网络提供商之前，必须显式启用 MB 订阅可以使用提供程序的服务相关。 术语*激活*是特定于设置基于 GSM 的 (GPRS/边缘/UMTS/HSDPA/t D-SCDMA) 技术的连接。 例如， *PDP 上下文激活*指设置 MB 连接根据 PDP 上下文中指定的参数。

*SIM 访问*指在访问用户识别模块 (SIM 中，也称为 R UIM)。 如果 MB 设备没有 SIM/R-UIM 作为物理实体，但改为具有逻辑等效项嵌入在设备中，此术语也适用于该逻辑线路等效。 不需要 SIM 访问时，微型端口驱动程序不应从 SIM 检索的信息，若要完成该请求。

### <a name="semantics"></a>语义

在用户模式下的 MB 服务组件不能直接交换 MB 微型端口驱动程序在内核模式下使用的数据。 例如 WMI 中介或[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)所需。 为简单起见，这些中介不显式本文档中讨论。 但是，此省略的方式并不意味着 MB 服务和 MB 微型端口驱动程序可以参与直接数据交换。

以下主题提供支持的移动宽带的驱动程序模型的操作的概述和摘要 NDIS 6.20 和 MB OID 语义，微型端口驱动程序执行同步和异步操作时必须遵循的过程：

[MB / NDIS 6.20 交互概述](mb---ndis-6-20-interfacing-overview.md)

[MB 数据模型](mb-data-model.md)

[MB 的操作语义](mb-operational-semantics.md)

[MB 驱动程序模型版本控制](mb-driver-model-versioning.md)

[MB 微型端口驱动程序 INF 要求](mb-miniport-driver-inf-requirements.md)

[MB 微型端口驱动程序类型](mb-miniport-driver-types.md)

[MB 适配器常规特性需求](mb-adapter-general-attribute-requirements.md)

[MB 原始 IP 数据包处理支持](mb-raw-ip-packet-processing-support.md)

[MB 微型端口驱动程序 IP 地址通知的准则](guidelines-for-mb-miniport-driver-ip-address-notifications.md)

[MB 微型端口驱动程序错误日志记录](mb-miniport-driver-error-logging.md)

[MB 微型端口驱动程序性能要求](mb-miniport-driver-performance-requirements.md)

 

 





