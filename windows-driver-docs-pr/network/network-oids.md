---
title: 网络 Oid
description: 网络 Oid
ms.assetid: a897ba37-7984-455f-9428-a74850f7e3b6
keywords:
- Oid WDK 网络
- 网络 Oid WDK
- 对象标识符 WDK 网络
- 有关 Oid 的 Oid WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d522a11e461d65e3783798ef792160020ec30931
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525680"
---
# <a name="network-oids"></a>网络 Oid





微型端口驱动程序维护其功能和当前状态有关的信息，以及它所管理的每个微型端口适配器有关的信息。 每种信息类型的对象标识符 (OID) 标识。 Oid 是系统定义的。 NDIS 处理许多微型端口驱动程序的 OID 请求和 NDIS 不会传递到微型端口驱动程序的此类请求。 微型端口驱动程序报告了许多以前未响应 OID 查询，在初始化过程中的属性报告其功能。 有关报告属性的详细信息，请参阅[初始化适配器](initializing-a-miniport-adapter.md)。

NDIS 和更高级别驱动程序可以查询和，使用 Oid，在某些情况下，设置的信息。

-   更高级别的驱动程序的无连接媒体调用[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)查询或无连接的微型端口驱动程序中设置的信息。 若要执行的查询或设置操作中，NDIS 调用微型端口驱动程序[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数。

-   更高级别的驱动程序为面向连接的媒体调用[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)查询或面向连接的微型端口驱动程序中设置的信息。 若要执行这两个查询和设置操作，NDIS 调用微型端口驱动程序[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数。

NDIS 将微型端口驱动程序的系统定义的 Oid 的许多映射到全局唯一标识符 (Guid)。 NDIS 注册这些 Guid 支持用户模式下基于 Web 的企业管理 (WBEM) 的应用程序使用内核模式 Microsoft Windows Management Instrumentation (WMI)。 如果 WMI 客户端查询，或设置一个这些 Guid，NDIS 将查询 OID 操作或设置 OID 操作中的，根据需要，请求并随后将传递任何返回的信息和状态回 WMI。 可以将自定义 Guid 映射到自定义 Oid 或微型端口驱动程序状态。 微型端口驱动程序必须注册自定义 GUID 的 OID 或 GUID 状态映射 NDIS 在初始化过程。

有关查询和设置 Oid，创建自定义 Oid 的详细信息和 NDIS 支持 WMI，请参阅[获取和设置微型端口驱动程序信息和 wmi 支持 NDIS](obtaining-and-setting-miniport-driver-information-and-ndis-support-for.md)。

 

 





