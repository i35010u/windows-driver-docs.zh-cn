---
title: NIC 交换机
description: NIC 交换机
ms.assetid: 7681DBB2-6645-4B06-9D95-64E7FD379029
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e010a225adcdd610b42d8f523d2e848a4b79362
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380588"
---
# <a name="nic-switches"></a>NIC 交换机


支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器必须实现之间的物理端口在适配器上和内部网络流量都转发的硬件桥梁[虚拟端口 (VPorts)](virtual-ports--vports-.md)。 此桥称为*NIC 交换机*并在下图中所示。

![显示与管理父分区的 sr-iov 适配器，并包含来宾操作系统的两个子分区的堆栈关系图](images/sriovarchitecture.png)

每个 NIC 交换机包含以下组件：

-   一个外部或*物理*，提供到外部物理网络的网络连接的端口。

-   PCI Express (PCIe) 物理函数 (PF) 网络适配器提供访问权限外部物理网络的一个内部端口。 内部端口被称为*虚拟端口 (VPort)*。

    PF 始终具有 VPort 创建并分配给它。 此 VPort 称为*默认 VPort*，并且默认情况下引用\_VPORT\_ID 标识符。

    有关 VPorts 详细信息，请参阅[虚拟端口 (VPorts)](virtual-ports--vports-.md)。

-   一个或多个 VPorts PCIe 虚拟函数 (VF) 网络适配器提供对外部物理网络访问权限。

    **请注意**  可以创建其他 VPorts，并将其分配给为网络访问 PF。

     

**请注意**  开头 NDIS 6.30 Windows Server 2012 中，SR-IOV 接口只支持一个 NIC 切换上的网络适配器。 此交换机被称为*默认 NIC 开关*，并引用的 NDIS\_默认\_切换\_ID 标识符。

 

SR-IOV 网络适配器的 PF 微型端口驱动程序由管理 NIC 交换机的硬件资源。 该驱动程序创建，并通过以下方法之一配置 NIC 开关：

-   静态创建将基于标准化 SR-IOV 和 NIC 交换机 INF 关键字。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   动态创建基于对象标识符 (OID) 的方法请求[OID\_NIC\_交换机\_创建\_开关](https://msdn.microsoft.com/library/windows/hardware/hh451815)。 NDIS 或 HYPER-V 可扩展交换机模块发出这些 OID 请求 SR-IOV 网络适配器上创建 NIC 开关。

有关如何创建、 配置和管理 NIC 开关的详细信息，请参阅[管理 NIC 开关](managing-nic-switches.md)。

 

 





