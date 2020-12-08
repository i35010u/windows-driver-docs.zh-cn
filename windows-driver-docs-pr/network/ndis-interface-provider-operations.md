---
title: NDIS 接口提供程序操作
description: NDIS 接口提供程序操作
keywords:
- NDIS 网络接口 WDK，接口提供程序
- 网络接口 WDK，接口提供程序
- 接口提供程序 WDk 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79884e07fc933b0e01e10f23bdb7e5215391c633
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798021"
---
# <a name="ndis-interface-provider-operations"></a>NDIS 接口提供程序操作





所有 NDIS 驱动程序都可以注册为接口提供程序。 每当驱动程序 (或 NDIS 代理接口提供程序) 检测到要引入到计算机的新接口时，它都会分配 [**NET \_ LUID**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) 索引，注册接口，并将关联的 NET \_ luid 值保留在持久性存储中 (如注册表) 。 以下列表描述了如何将新接口引入计算机的几个示例：

-   安装网络适配器，无论是用于中间驱动程序的虚拟适配器还是物理适配器。 在这种情况下，NDIS 代理接口提供程序管理接口。

-   附加筛选器模块。 在这种情况下，NDIS 代理接口提供程序管理接口。

-   MUX 中间驱动程序内部绑定。 MUX 中间驱动程序应该实现 NDIS 提供程序服务来处理这种情况，因为内部接口对 NDIS 不可见。

当计算机重新启动时，如果接口是持久的，则接口提供程序不应为同一接口分配新的 [**net \_ luid**](/windows/win32/api/ifdef/ns-ifdef-net_luid_lh) ; 相反，接口提供程序应使用之前存储的 net \_ luid 值注册同一接口。 此外，即使接口不是持久的，接口提供程序也必须释放 NET \_ LUID 索引（如果存在计算机电源故障）。 因此，接口提供程序应将 NET \_ LUID 存储在持久性存储中 (例如，注册表) 。

如果接口提供程序检测到接口正在关闭，则它应取消注册接口。

**注意**  当卸载微型端口适配器时，NDIS 代理提供程序注销接口，并在分离时筛选模块。

 

如果接口提供程序检测到已完全删除某个接口 (例如，NDIS 代理提供程序将收到) 卸载微型端口适配器的通知，接口提供程序会注销接口并释放 NET \_ LUID 索引。 当分离筛选器模块时，NDIS 代理提供程序还会释放 NET \_ LUID 索引。

在运行时，接口提供程序为其注册的接口处理 OID 请求。 NDIS 代理接口提供程序可能会向底层驱动程序发出 OID 请求，以获取接口信息。

 

