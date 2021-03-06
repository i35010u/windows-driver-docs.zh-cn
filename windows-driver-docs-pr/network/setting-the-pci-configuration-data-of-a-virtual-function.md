---
title: 设置虚拟功能的 PCI 配置数据
description: 设置虚拟功能的 PCI 配置数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663e21ff8ba2d985c52205a9d8c37a50608055ae
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248964"
---
# <a name="setting-the-pci-configuration-data-of-a-virtual-function"></a>设置虚拟功能的 PCI 配置数据


PCI Express (PCIe) 虚函数 () VF 的微型端口驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 因此，VF 微型端口驱动程序无法直接访问硬件资源，如 VF 的 PCI 配置空间。 只有 PCIe 物理功能 (PF) 的微型端口驱动程序可以访问 VF 的 PCI 配置空间。 PF 微型端口驱动程序在 Hyper-v 父分区的管理操作系统中运行，并具有对 VF 资源的特权访问权限。

当 VF 微型端口驱动程序调用 [**NdisMSetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)来写入 PCI 配置空间时，占用了虚拟化堆栈（如虚拟化堆栈）的 oid 集请求会发出 oid [ \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间](./oid-sriov-write-vf-config-space.md)的 oid 设置请求。

在发出此 OID 集请求之前，过量驱动程序必须按以下方式设置 [**NDIS \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters) 结构的成员：

-   将 **VFId** 成员设置为要为其写入信息的 VF 的标识符。

-   将 **偏移** 成员设置为要在其中写入数据的 VF 的 PCI 配置空间内的偏移量。

-   将 **Length** 成员设置为要写入 VF 的 PCI 配置空间的字节数。

-   将 **BufferOffset** 成员设置为缓冲区内的偏移量 (**) 成员将** 包含写入指定 VF 的 PCI 配置空间的数据。 此偏移量是以字节数为单位的，从 [**NDIS \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间 \_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters) 的结构开始。

当它处理 [oid \_ SRIOV \_ WRITE \_ VF \_ 配置 \_ 空间](./oid-sriov-write-vf-config-space.md)的 oid 方法请求时，PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 [**NDIS \_ SRIOV \_ WRITE \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)结构的 **VFId** 成员指定的 VF 是否包含以前分配的资源。 PF 微型端口驱动程序通过 oid [ \_ NIC \_ 交换机 \_ 分配 \_ vf](./oid-nic-switch-allocate-vf.md)的 oid 方法请求为 VF 分配资源。

    如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   PF 微型端口驱动程序调用 [**NdisMSetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata) 来写入请求的 PCI 配置空间。 但是，PF 微型端口驱动程序还可以返回该驱动程序从 PCI 配置空间的先前读取或写入操作中缓存的 VF 的 PCI 配置空间数据。

    **注意**  如果独立硬件供应商 (IHV) 提供一个虚拟总线驱动程序 (VBD) 作为其 SR-IOV [驱动程序包](../install/driver-packages.md)的一部分，则它的 PF 微型端口驱动程序不得调用 [**NdisMSetVirtualFunctionBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)。 相反，驱动程序必须通过专用信道与 VBD 交互，并请求该 VBD 调用 [*SetVirtualFunctionData*](/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)。 此函数从底层虚拟 PCI (VPCI) 总线驱动程序支持的 [GUID \_ VPCI \_ 接口 \_ 标准](https://msdn.microsoft.com/library/windows/hardware/hh451146) 接口公开。

     

如果 PF 微型端口驱动程序能够成功完成 OID 请求，则驱动程序必须将请求的 PCI 配置空间数据复制到 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员所引用的缓冲区。 驱动程序将数据复制到由 [**NDIS \_ SRIOV \_ READ \_ VF \_ CONFIG \_ SPACE \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构的 **BufferOffset** 成员指定的偏移量处的缓冲区。

 

