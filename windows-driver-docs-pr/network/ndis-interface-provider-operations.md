---
title: NDIS 接口提供程序操作
description: NDIS 接口提供程序操作
ms.assetid: cd5c76b0-6b38-44ea-ac1b-02be5d073203
keywords:
- NDIS 网络接口 WDK，接口提供程序
- 网络接口 WDK，接口提供程序
- 接口提供程序 WDk 网络接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b00e6d204951aebb8471c11e49b396ac5e7cf5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385511"
---
# <a name="ndis-interface-provider-operations"></a>NDIS 接口提供程序操作





所有的 NDIS 驱动程序可以将注册为接口提供程序。 每当一个驱动程序 （或 NDIS 代理接口提供程序） 检测到新的接口，已引入到计算机，它会分配[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)索引，注册接口，并保留关联的 NET\_LUID 持久存储 （如注册表） 中的值。 以下列表描述了几个示例的新接口可以引入到计算机的方式：

-   可以安装的网络适配器，中间驱动程序的虚拟适配器或物理适配器。 在这种情况下，NDIS 代理接口提供程序管理接口。

-   将附加筛选器模块。 在这种情况下，NDIS 代理接口提供程序管理接口。

-   MUX 中间驱动程序的内部绑定。 MUX 中间驱动程序应实现 NDIS 提供程序服务来处理这种情况下，因为内部接口看不到 NDIS。

计算机随后重新启动时，接口提供程序不应分配一个新[ **NET\_LUID** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-net_luid_lh)为同一接口的接口是持久的; 如果相反，该接口提供程序应使用以前存储的 NET\_要注册的相同接口的 LUID 值。 此外，即使该接口不是永久性的接口提供程序必须释放 NET\_LUID 索引计算机电源故障时。 因此，接口提供程序应存储 NET\_持久存储 （例如，注册表） 中的 LUID。

如果接口提供程序检测到一个接口，正在关闭，它应取消注册，该接口。

**请注意**  NDIS 代理提供程序注销微型端口适配器的接口，它们都会被卸载并分离时筛选模块时。

 

如果检测到的接口提供完全删除接口 （例如，NDIS 代理提供程序通知正在卸载的微型端口适配器），接口提供程序注销该接口，并释放 NET\_LUID 的索引。 NDIS 代理提供程序也会释放 NET\_LUID 索引时分离筛选器模块。

在运行时接口提供程序处理接口的已注册的 OID 的请求。 NDIS 代理接口提供程序可能会向基础驱动程序，以获取接口的信息发出 OID 的请求。

 

 





