---
title: 查询虚拟功能的 PCI 配置空间
description: 查询虚拟功能的 PCI 配置空间
ms.assetid: FFE7C946-4406-46A5-A9A7-CD0E2756C98E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb5382b2d51fb6915f35e3dff3984aa61dfef0e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216970"
---
# <a name="querying-the-pci-configuration-space-for-a-virtual-function"></a>查询虚拟功能的 PCI 配置空间

**注意** 此方法只能由 Hyper-v 父分区的管理操作系统中运行的过量驱动程序使用。

PCI Express (PCIe) 虚函数 () VF 的微型端口驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 因此，VF 微型端口驱动程序无法直接访问硬件资源，如 VF 的 PCIe 配置空间。 只有 PCIe 物理功能 (PF) 的微型端口驱动程序可以访问 VF 的 PCIe 配置空间。 PF 微型端口驱动程序在 Hyper-v 父分区的管理操作系统中运行，并具有对 VF 资源的特权访问权限。

在管理操作系统中运行的过量驱动程序会发出 (OID) 方法请求中的对象标识符 [， \_ \_ 读取 \_ VF 配置 \_ \_ 空间](./oid-sriov-read-vf-config-space.md) 以便从网络适配器上指定的 VF 读取 PCIe 配置空间中的数据。

例如，在管理操作系统中运行的虚拟化堆栈发出 oid 方法请求：当 VF 微型端口驱动程序调用[**NdisMGetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)从其 VF PCIe 配置空间读取时， [ \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间](./oid-sriov-read-vf-config-space.md)。

在发出此 OID 方法请求之前，过量驱动程序必须按以下方式设置[**NDIS \_ SRIOV \_ READ \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters) 结构的成员：

-   **VFId**成员必须设置为要从中读取信息的 VF 的标识符。

-   **偏移**成员必须设置为要在其中读取数据的 VF 的 PCIe 配置空间内的偏移量。

-   **长度**成员必须设置为要从 VF 的 PCIe 配置空间中读取的字节数。

-   **BufferOffset**成员必须设置为缓冲区内的偏移量 (**) 成员将**包含从指定的 VF PCI 配置空间读取的数据。 此偏移量是以字节数为单位的，从 [**NDIS \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters) 结构开始。

当它处理 [oid \_ SRIOV \_ READ \_ VF \_ 配置 \_ 空间](./oid-sriov-read-vf-config-space.md)的 oid 方法请求时，PF 微型端口驱动程序必须遵循以下准则：

-   微型端口驱动程序必须验证由[**NDIS \_ SRIOV \_ \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)的**VFId**成员指定的 vf 是否具有以前分配的资源。 微型端口驱动程序通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)的 oid 方法请求为 VF 分配资源。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   微型端口驱动程序必须验证 ([**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)) 结构的**InformationBuffer**成员引用的缓冲区是否足够大，以便返回请求的 PCIe 配置空间数据。 如果不是这样，则驱动程序必须使 OID 请求失败。
-   小型端口驱动程序通常会调用 [**NdisMGetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata) 来查询请求的 PCIe 配置空间。 但是，微型端口驱动程序还可以返回该程序已缓存的 VF 配置空间的配置空间数据。

    **注意**   如果独立硬件供应商 (IHV) 提供 (的 VBD) 作为其 SR-IOV[驱动程序包](../install/driver-packages.md)的一部分的虚拟总线驱动程序，则其微型端口驱动程序不得调用[**NdisMGetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)。 相反，驱动程序必须通过专用信道与 VBD 交互，并请求该 VBD 调用 [*ReadVfConfigBlock*](/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))。 此函数从底层虚拟 PCI (VPCI) 总线驱动程序支持的 [GUID \_ VPCI \_ 接口 \_ 标准](https://msdn.microsoft.com/library/windows/hardware/hh451146) 接口公开。

     

成功从此 OID 方法请求返回后， [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS \_ SRIOV \_ 读取 vf 配置 \_ \_ \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构，其中包含 VF 的 PCIe 配置空间读取操作的参数。

-   要从 PCIe 配置空间读取的数据的额外缓冲空间。 驱动程序将数据复制到由[**NDIS \_ SRIOV \_ READ \_ VF \_ CONFIG \_ SPACE \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构的**BufferOffset**成员指定的偏移量处的缓冲区。

 

