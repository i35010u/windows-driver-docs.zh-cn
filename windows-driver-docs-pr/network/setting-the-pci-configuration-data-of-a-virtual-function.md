---
title: 设置虚拟功能的 PCI 配置数据
description: 设置虚拟功能的 PCI 配置数据
ms.assetid: 74CAAD8B-7009-4C79-A496-93B4A3DA0B43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdedf519882ba93dc54ff91dc5c733f1cffa66f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841931"
---
# <a name="setting-the-pci-configuration-data-of-a-virtual-function"></a>设置虚拟功能的 PCI 配置数据


PCI Express （PCIe）虚拟功能（VF）的微型端口驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 因此，VF 微型端口驱动程序无法直接访问硬件资源，如 VF 的 PCI 配置空间。 只有 PCIe 物理功能（PF）的微型端口驱动程序可以访问 VF 的 PCI 配置空间。 PF 微型端口驱动程序在 Hyper-v 父分区的管理操作系统中运行，并具有对 VF 资源的特权访问权限。

占用大量的驱动程序（例如虚拟化堆栈）发出 oid\_SRIOV 的 OID 集请求\_在 VF 微型端口驱动程序调用[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)写入其 PCI 配置空间时， [\_配置\_空间写入\_vf](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space) 。

在发出此 OID 集请求之前，过量驱动程序必须将 NDIS\_SRIOV 的成员设置\_通过以下方式[ **\_配置\_参数结构写入\_VF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters):\_

-   将**VFId**成员设置为要为其写入信息的 VF 的标识符。

-   将**偏移**成员设置为要在其中写入数据的 VF 的 PCI 配置空间内的偏移量。

-   将**Length**成员设置为要写入 VF 的 PCI 配置空间的字节数。

-   将**BufferOffset**成员设置为缓冲区内的偏移量（由**InformationBuffer**成员引用），该偏移量将包含写入指定 VF 的 PCI 配置空间的数据。 此偏移量是以字节为单位指定的，从[**NDIS\_SRIOV 开始，\_写入\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)结构。

当处理 Oid\_SRIOV 的 OID 方法请求时[\_写入\_VF\_配置\_空间](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-write-vf-config-space)，则 PF 微型端口驱动程序必须遵循以下准则：

-   PF 微型端口驱动程序必须验证由 NDIS\_SRIOV 的**VFId**成员指定的 VF [ **\_写入\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters)结构是否包含之前已有的资源分配. PF 微端口驱动程序通过 oid 的 oid 方法请求为 VF 分配资源[\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。

    如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   PF 微型端口驱动程序调用[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)来写入请求的 PCI 配置空间。 但是，PF 微型端口驱动程序还可以返回该驱动程序从 PCI 配置空间的先前读取或写入操作中缓存的 VF 的 PCI 配置空间数据。

    **请注意**  如果独立硬件供应商（IHV）提供了虚拟总线驱动程序（VBD）作为其 sr-iov[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)的一部分，则它的 PF 微型端口驱动程序不得调用[**NdisMSetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetvirtualfunctionbusdata)。 相反，驱动程序必须通过专用信道与 VBD 交互，并请求该 VBD 调用[*SetVirtualFunctionData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_virtual_device_data)。 此函数由基础虚拟 PCI （VPCI）总线驱动程序所支持的[GUID\_VPCI\_接口\_标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)接口公开。

     

如果 PF 微型端口驱动程序能够成功完成 OID 请求，则驱动程序必须将所请求的 PCI 配置空间数据复制到[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员引用的缓冲区. 驱动程序会将数据复制到 NDIS\_SRIOV 的**BufferOffset**成员指定的偏移量处的缓冲区， [ **\_读取\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构。

 

 





