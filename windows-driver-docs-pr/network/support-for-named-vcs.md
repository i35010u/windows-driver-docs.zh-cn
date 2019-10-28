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
ms.openlocfilehash: 4039d70d9117bb40d86f3e9e7f3df53e85368b8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841801"
---
# <a name="support-for-named-vcs"></a>命名 VC 的支持





NDIS 允许 WMI 客户端查询和设置面向连接的小型端口适配器的每个虚拟连接（VC）的信息。 WMI 客户端还可以枚举 VCs。 在 WMI 客户端可以查询或设置与特定的 VC 关联的信息之前，独立调用管理器或面向连接的客户端必须通过调用[**NdisCoAssignInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename)函数来命名 VC。

独立调用管理器或面向连接的客户端通过调用[**NdisCoCreateVC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)函数启动了 vc 设置后，独立调用管理器或面向连接的客户端可以使用**NDISCOASSIGNINSTANCENAME**来命名 vc。 NDIS 为 VC 指定实例名称，并将实例名称注册到 WMI。 然后，WMI 客户端可以枚举 VC 和查询或设置相对于 VC 的 Oid。

微型端口调用管理器（MCM）不能使用[**NdisCoAssignInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename)来命名其 VCs。 相反，MCM 应为 VC 创建自定义 GUID 和 OID，并使用 NDIS 注册 GUID 到 OID 的映射。 有关注册自定义 Oid 的详细信息，请参阅[自定义 oid 和状态指示](customized-oids-and-status-indications.md)。

 

 





