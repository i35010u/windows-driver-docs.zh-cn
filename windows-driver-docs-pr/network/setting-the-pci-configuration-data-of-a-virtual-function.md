---
title: 设置虚拟功能的 PCI 配置数据
description: 设置虚拟功能的 PCI 配置数据
ms.assetid: 74CAAD8B-7009-4C79-A496-93B4A3DA0B43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7fcadadbc051005d0ae467cf986bb93731da5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362025"
---
# <a name="setting-the-pci-configuration-data-of-a-virtual-function"></a>设置虚拟功能的 PCI 配置数据


微型端口驱动程序为 PCI Express (PCIe) 虚拟函数 (VF) 在运行 HYPER-V 子分区的来宾操作系统中。 正因为如此，VF 微型端口驱动程序不能直接访问硬件资源，例如 VF PCI 配置空间。 仅微型端口驱动程序 PCIe 物理函数 (PF) 为可访问以 VF PCI 配置空间。 PF 微型端口驱动程序管理操作系统的 HYPER-V 父分区中运行，并具有特权 VF 资源的访问权限。

基础驱动程序，如虚拟化堆栈中，颁发的 OID 集请求[OID\_SRIOV\_编写\_VF\_CONFIG\_空间](https://msdn.microsoft.com/library/windows/hardware/hh451925)时 VF 微型端口驱动程序调用[ **NdisMSetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff563670)要写入到其 PCI 配置空间。

它会发出此 OID 集请求之前，基础驱动程序必须设置的成员[**NDIS\_SRIOV\_编写\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451688)结构如下所示：

-   设置**VFId**成员添加到为其的信息是要写入的 VF 的标识符。

-   设置**偏移量**成员添加到要在其中写入数据的 VF PCI 配置空间内的偏移量。

-   设置**长度**成员添加到的字节数写入 VF PCI 配置空间。

-   设置**BufferOffset**成员添加到缓冲区中的偏移量 (由引用**InformationBuffer**成员)，将包含的数据写入到指定的 VF PCI 配置空间。 从开始处的以字节为单位指定此偏移量[ **NDIS\_SRIOV\_编写\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451688)结构。

当它处理的 OID 方法请求[OID\_SRIOV\_编写\_VF\_CONFIG\_空间](https://msdn.microsoft.com/library/windows/hardware/hh451925)，PF 微型端口驱动程序必须遵循这些准则：

-   PF 微型端口驱动程序必须验证指定 VF **VFId**的成员[ **NDIS\_SRIOV\_编写\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451688)结构，具有先前已分配的资源。 PF 微型端口驱动程序分配资源，用于通过 OID 方法请求的 VF [OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814)。

    如果尚未分配指定 VF 的资源的驱动程序必须失败 OID 请求。

-   PF 微型端口驱动程序调用[ **NdisMSetVirtualFunctionBusData** ](https://msdn.microsoft.com/library/windows/hardware/hh451526)要写入到请求的 PCI 配置空间。 但是，PF 微型端口驱动程序还可以返回驱动程序已从以前缓存的 VF PCI 配置空间数据读取或写入操作的 PCI 配置空间。

    **请注意**  如果的独立硬件供应商 (IHV) 提供虚拟总线驱动程序 (VBD) 作为其 SR-IOV 的一部分[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)，不能调用其 PF 微型端口驱动程序[ **NdisMSetVirtualFunctionBusData**](https://msdn.microsoft.com/library/windows/hardware/hh451526)。 相反，该驱动程序必须与通过专用通信通道，VBD 接口，并请求，调用 VBD [ *SetVirtualFunctionData*](https://msdn.microsoft.com/library/windows/hardware/hh451552)。 此函数从其公开[GUID\_VPCI\_界面\_标准](https://msdn.microsoft.com/library/windows/hardware/hh451146)基础的虚拟 PCI (VPCI) 总线驱动程序支持的接口。

     

如果 PF 微型端口驱动程序才能成功完成 OID 请求，该驱动程序必须请求的 PCI 配置空间数据复制到引用的缓冲区**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 该驱动程序将数据复制到指定的偏移量处的缓冲区**BufferOffset**的成员[ **NDIS\_SRIOV\_读取\_VF\_配置\_空间\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451681)结构。

 

 





