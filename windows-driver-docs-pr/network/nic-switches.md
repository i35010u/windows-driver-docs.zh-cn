---
title: NIC 交换机
description: NIC 交换机
ms.assetid: 7681DBB2-6645-4B06-9D95-64E7FD379029
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f661ef96df5c5a8088fa212c26444041cd2144cd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216156"
---
# <a name="nic-switches"></a>NIC 交换机


支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器必须实现一个硬件桥，该桥将适配器上的物理端口与内部 [虚拟端口 (VPorts) ](virtual-ports--vports-.md)之间的网络流量转发。 此桥称为 *NIC 交换机* ，如下图所示。

![显示具有管理父分区和包含来宾操作系统的两个子分区的 sr-iov 适配器的堆栈关系图](images/sriovarchitecture.png)

每个 NIC 交换机包含以下组件：

-   一个外部端口或 *物理*端口，提供与外部物理网络的网络连接。

-   一个内部端口，提供 PCI Express (PCIe) 物理功能 (PF 在网络适配器上) ，并可访问外部物理网络。 内部端口称为 *虚拟端口 (VPort) *。

    PF 始终具有创建并分配给它的 VPort。 此 VPort 称为 *默认 VPort*，由默认的 \_ VPort \_ ID 标识符引用。

    有关 VPorts 的详细信息，请参阅 [虚拟端口 (VPorts) ](virtual-ports--vports-.md)。

-   一个或多个 VPorts 提供了一个或多个 (VF) 网络适配器上的虚拟机的访问权限，该功能可访问外部物理网络。

    **注意**   可以创建其他 VPorts，并将其分配到 PF 进行网络访问。

     

**注意**   从 Windows Server 2012 中的 NDIS 6.30 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为 *默认 NIC 交换机*，由 NDIS \_ 默认 \_ 交换机 \_ ID 标识符引用。

 

NIC 交换机的硬件资源由 SR-IOV 网络适配器的 PF 微型端口驱动程序管理。 驱动程序通过以下方法之一创建和配置 NIC 交换机：

-   基于标准化 SR-IOV 和 NIC 交换机 INF 关键字的静态创建。 有关这些关键字的详细信息，请参阅 [sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   基于对象标识符的动态创建 (oid [ \_ NIC \_ 交换机 \_ CREATE \_ SWITCH](./oid-nic-switch-create-switch.md)) 方法请求。 NDIS 或 Hyper-v 可扩展交换机模块发出这些 OID 请求，以在 SR-IOV 网络适配器上创建 NIC 交换机。

有关如何创建、配置和管理 NIC 交换机的详细信息，请参阅 [管理 Nic 交换机](managing-nic-switches.md)。

 

