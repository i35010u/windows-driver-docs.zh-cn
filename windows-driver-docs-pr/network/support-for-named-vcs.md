---
title: 命名 VC 的支持
description: 命名 VC 的支持
ms.assetid: 797f737c-91e7-410b-91d5-5575d5b19e86
keywords:
- WMI WDK 网络，虚拟连接
- 呼叫经理 WDK 网络，命名虚拟连接
- 虚拟连接 WDK NDIS WMI
- VCs WDK NDIS WMI
- 微型端口呼叫管理器 WDK 网络，命名虚拟连接
- MCMs WDK 网络，namin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5588ddabc2f2264e930d7c404c458eebcab13ab5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207405"
---
# <a name="support-for-named-vcs"></a>命名 VC 的支持





NDIS 允许 WMI 客户端查询和设置面向连接的小型端口适配器 (VC) 基础的每个虚拟连接的信息。 WMI 客户端还可以枚举 VCs。 在 WMI 客户端可以查询或设置与特定的 VC 关联的信息之前，独立调用管理器或面向连接的客户端必须通过调用 [**NdisCoAssignInstanceName**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename) 函数来命名 VC。

独立调用管理器或面向连接的客户端通过调用 [**NdisCoCreateVC**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc) 函数启动了 vc 设置后，独立调用管理器或面向连接的客户端可以使用 **NDISCOASSIGNINSTANCENAME**来命名 vc。 NDIS 为 VC 指定实例名称，并将实例名称注册到 WMI。 然后，WMI 客户端可以枚举 VC 和查询或设置相对于 VC 的 Oid。

小型端口调用管理器 (MCM) 不能使用 [**NdisCoAssignInstanceName**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename) 来命名其 VCs。 相反，MCM 应为 VC 创建自定义 GUID 和 OID，并使用 NDIS 注册 GUID 到 OID 的映射。 有关注册自定义 Oid 的详细信息，请参阅 [自定义 oid 和状态指示](customized-oids-and-status-indications.md)。

 

