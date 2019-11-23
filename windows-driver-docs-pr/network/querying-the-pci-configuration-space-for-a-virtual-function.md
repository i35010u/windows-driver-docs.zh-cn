---
title: 查询虚拟功能的 PCI 配置空间
description: 查询虚拟功能的 PCI 配置空间
ms.assetid: FFE7C946-4406-46A5-A9A7-CD0E2756C98E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2d042950837655d8fdd253ee1054cca137ddc41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844871"
---
# <a name="querying-the-pci-configuration-space-for-a-virtual-function"></a>查询虚拟功能的 PCI 配置空间

**注意**此方法只能由 Hyper-v 父分区的管理操作系统中运行的过量驱动程序使用。

PCI Express （PCIe）虚拟功能（VF）的微型端口驱动程序在 Hyper-v 子分区的来宾操作系统中运行。 因此，VF 微型端口驱动程序无法直接访问硬件资源，如 VF 的 PCIe 配置空间。 只有 PCIe 物理功能（PF）的微型端口驱动程序可以访问 VF 的 PCIe 配置空间。 PF 微型端口驱动程序在 Hyper-v 父分区的管理操作系统中运行，并具有对 VF 资源的特权访问权限。

在管理操作系统中运行的过量驱动程序会发出 OID 的对象标识符（OID）方法请求[\_SRIOV\_读取\_VF\_配置\_空间](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)，以便从网络适配器上指定的 Vf 读取 PCIe 配置空间中的数据。

例如，在管理操作系统中运行的虚拟化堆栈发出 oid 的 OID 方法请求\_SRIOV\_在 VF 微型端口驱动程序调用[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)从其 VF PCIe 配置空间读取时[\_配置\_空间读取\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space) 。

在发出此 OID 方法请求之前，过量驱动程序必须将 NDIS\_SRIOV 的成员设置\_通过以下方式[ **\_配置\_参数结构读取\_VF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters) ：\_

-   **VFId**成员必须设置为要从中读取信息的 VF 的标识符。

-   **偏移**成员必须设置为要在其中读取数据的 VF 的 PCIe 配置空间内的偏移量。

-   **长度**成员必须设置为要从 VF 的 PCIe 配置空间中读取的字节数。

-   **BufferOffset**成员必须设置为缓冲区内的偏移量（由**InformationBuffer**成员引用），该偏移量将包含从指定的 VF 的 PCI 配置空间读取的数据。 此偏移量是以字节数为单位指定的，从[**NDIS\_SRIOV 的开始\_读取\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构。

当它处理 Oid\_SRIOV 的 OID 方法请求时[\_读取\_VF\_配置\_空间](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-read-vf-config-space)，PF 微型端口驱动程序必须遵循以下准则：

-   微型端口驱动程序必须验证由 NDIS\_SRIOV 的**VFId**成员指定的 VF [ **\_读取\_vf\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构是否包含之前已分配的资源。 微型端口驱动程序通过 oid 的 oid 方法请求为 VF 分配资源[\_NIC\_交换机\_分配\_VF](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-allocate-vf)。 如果没有为指定的 VF 分配资源，则驱动程序必须使 OID 请求失败。

-   微型端口驱动程序必须验证缓冲区（由[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员引用）足够大，可以返回请求的 PCIe 配置空间数据。 如果不是这样，则驱动程序必须使 OID 请求失败。
-   小型端口驱动程序通常会调用[**NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)来查询请求的 PCIe 配置空间。 但是，微型端口驱动程序还可以返回该程序已缓存的 VF 配置空间的配置空间数据。

    **请注意**  如果独立硬件供应商（IHV）提供了虚拟总线驱动程序（VBD）作为其 sr-iov[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)的一部分，则其微型端口驱动程序不得调用[**NdisMGetVirtualFunctionBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetvirtualfunctionbusdata)。 相反，驱动程序必须通过专用信道与 VBD 交互，并请求该 VBD 调用[*ReadVfConfigBlock*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh439637(v=vs.85))。 此函数由基础虚拟 PCI （VPCI）总线驱动程序所支持的[GUID\_VPCI\_接口\_标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)接口公开。

     

成功从此 OID 方法请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向调用方分配的缓冲区的指针。 此缓冲区的格式设置为包含以下内容：

-   [**NDIS\_SRIOV\_读取\_vf\_配置\_空间\_个参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构，其中包含 VF 的 PCIe 配置空间读取操作的参数。

-   要从 PCIe 配置空间读取的数据的额外缓冲空间。 驱动程序会将数据复制到 NDIS\_SRIOV 的**BufferOffset**成员指定的偏移量处的缓冲区， [ **\_读取\_VF\_配置\_空间\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters)结构。

 

 





