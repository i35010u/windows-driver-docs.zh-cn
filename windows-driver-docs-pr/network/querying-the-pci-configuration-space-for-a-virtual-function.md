---
title: 查询虚拟功能的 PCI 配置空间
description: 查询虚拟功能的 PCI 配置空间
ms.assetid: FFE7C946-4406-46A5-A9A7-CD0E2756C98E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06f349161f8fd26a6b19a2a2cdb31f21a2b04dd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339991"
---
# <a name="querying-the-pci-configuration-space-for-a-virtual-function"></a>查询虚拟功能的 PCI 配置空间

**请注意**此方法只能由过量的 HYPER-V 父分区在管理操作系统中运行的驱动程序。

微型端口驱动程序为 PCI Express (PCIe) 虚拟函数 (VF) 在运行 HYPER-V 子分区的来宾操作系统中。 正因为如此，VF 微型端口驱动程序不能直接访问硬件资源，例如 VF PCIe 配置空间。 仅微型端口驱动程序 PCIe 物理函数 (PF) 为可访问以 VF PCIe 配置空间。 PF 微型端口驱动程序管理操作系统的 HYPER-V 父分区中运行，并具有特权 VF 资源的访问权限。

在管理操作系统中运行的基础驱动程序发出的一个对象标识符 (OID) 方法请求[OID\_SRIOV\_读取\_VF\_CONFIG\_空间](https://msdn.microsoft.com/library/windows/hardware/hh451879)为网络适配器上指定 VF 从 PCIe 配置空间读取数据。

例如，在管理操作系统中运行的虚拟化堆栈颁发的 OID 方法请求[OID\_SRIOV\_读取\_VF\_CONFIG\_空间](https://msdn.microsoft.com/library/windows/hardware/hh451879)VF 微型端口驱动程序在调用[ **NdisMGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563591)读取从其 VF PCIe 配置空间。

它会发出此 OID 方法请求之前，基础驱动程序必须设置的成员[**NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)结构如下所示：

-   **VFId**成员必须设置为 VF 是要读取信息的标识符。

-   **偏移量**成员必须设置为要从中读取数据的 VF PCIe 配置空间内的偏移量。

-   **长度**成员必须设置为的字节数，以从 VF PCIe 配置空间读取。

-   **BufferOffset**成员必须设置为缓冲区中的偏移量 (由引用**InformationBuffer**成员)，将包含从指定的 VF PCI 配置空间读取数据. 从开始处的以字节为单位指定此偏移量[ **NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)结构。

当它处理的 OID 方法请求[OID\_SRIOV\_读取\_VF\_CONFIG\_空间](https://msdn.microsoft.com/library/windows/hardware/hh451879)，PF 微型端口驱动程序必须遵循这些准则：

-   微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)结构，具有先前已分配的资源。 微型端口驱动程序分配资源，用于通过 OID 方法请求的 VF [OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。 如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

-   微型端口驱动程序必须验证缓冲区 (通过引用**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构） 是足以返回所请求的 PCIe 配置空间数据。 如果不为 true，则驱动程序必须失败 OID 请求。
-   微型端口驱动程序通常会调用[ **NdisMGetVirtualFunctionBusData** ](https://msdn.microsoft.com/library/windows/hardware/hh451484)查询请求的 PCIe 配置空间。 但是，从上一个已缓存了该驱动程序的 VF PCIe 配置空间数据读取或写入操作的 PCIe 配置空间，还可以返回微型端口驱动程序。

    **请注意**  如果的独立硬件供应商 (IHV) 提供虚拟总线驱动程序 (VBD) 作为其 SR-IOV 的一部分[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)，不能调用其微型端口驱动程序[ **NdisMGetVirtualFunctionBusData**](https://msdn.microsoft.com/library/windows/hardware/hh451484)。 相反，该驱动程序必须与通过专用通信通道，VBD 接口，并请求，调用 VBD [ *ReadVfConfigBlock*](https://msdn.microsoft.com/library/windows/hardware/hh439637)。 此函数从其公开[GUID\_VPCI\_界面\_标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)基础的虚拟 PCI (VPCI) 总线驱动程序支持的接口。

     

通过此 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含调用方分配的缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)结构，其中包含VF PCIe 配置空间的读取操作的参数。

-   要从 PCIe 配置空间读取的数据的附加缓冲区空间。 该驱动程序将数据复制到指定的偏移量处的缓冲区**BufferOffset**的成员[ **NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)结构。

 

 





