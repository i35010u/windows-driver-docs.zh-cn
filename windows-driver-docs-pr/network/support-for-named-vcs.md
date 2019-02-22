---
title: 对命名 VCs 的支持
description: 对命名 VCs 的支持
ms.assetid: 797f737c-91e7-410b-91d5-5575d5b19e86
keywords:
- WMI WDK 网络、 虚拟连接
- 调用连接网络、 命名虚拟连接管理器 WDK
- 虚拟连接 WDK NDIS WMI
- VCs WDK NDIS WMI
- 微型端口调用管理器 WDK 网络，命名虚拟连接
- MCMs WDK 网络 namin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b061c9832f77d1a9a7034a58b809d35a6e52afd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548191"
---
# <a name="support-for-named-vcs"></a>对命名 VCs 的支持





NDIS 允许 WMI 客户端查询并在每个虚拟连接 (VC) 基础上为面向连接的微型端口适配器设置信息。 WMI 客户端还可以枚举 VCs。 WMI 客户端可以查询或设置与特定 VC 相关联的信息之前，将独立呼叫管理器或面向连接的客户端必须命名为 VC 通过调用[ **NdisCoAssignInstanceName** ](https://msdn.microsoft.com/library/windows/hardware/ff561692)函数。

独立调用后管理器还是面向连接的客户端启动的 VC 安装程序通过调用[ **NdisCoCreateVC** ](https://msdn.microsoft.com/library/windows/hardware/ff561696)函数、 独立呼叫管理器或面向连接的客户端可以命名与 VC **NdisCoAssignInstanceName**。 NDIS 分配 VC 实例名称，并向 WMI 注册实例名称。 然后，WMI 客户端可以枚举 VC 和查询，或设置相对于 VC 的 Oid。

微型端口呼叫管理器 (MCM) 不能使用[ **NdisCoAssignInstanceName** ](https://msdn.microsoft.com/library/windows/hardware/ff561692)来命名其 VCs。 相反，MCM 应为 VC 创建自定义 GUID 和 OID 并使用 NDIS 注册 GUID OID 映射。 有关注册自定义 Oid 的详细信息，请参阅[自定义 Oid 和状态指示](customized-oids-and-status-indications.md)。

 

 





