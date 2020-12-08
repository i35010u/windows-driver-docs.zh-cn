---
title: 从 VF 微型端口驱动程序进行反向通道通信
description: 从 VF 微型端口驱动程序进行反向通道通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd4a85ed5a2a135015b2931ded2b25204dfebba8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813029"
---
# <a name="backchannel-communication-from-a-vf-miniport-driver"></a>从 VF 微型端口驱动程序进行反向通道通信


PCI Express (PCIe) 虚函数 (VF 的微型端口驱动程序) 与 PCIe 物理功能的微型端口驱动程序通信 (PF) 从 VF 配置块读取或写入数据。

VF 配置块用于 backchannel 和 VF 微型端口驱动程序之间的通信。 独立硬件供应商 (IHV) 可以定义设备的一个或多个 VF 配置块。 每个 VF 配置块都有一个 IHV 定义的格式、长度和块 ID。 例如，IHV 可以定义一个 VF 配置块，该配置块可用于媒体访问控制 (MAC) 地址的 VF 微型端口驱动程序。 其他 VF 配置块可用于当前 VF 和虚拟端口 (VPort) 配置。

**注意**  每个 VF 配置块中的数据仅用于 PF 和 VF 微型端口驱动程序。 此数据的格式和内容对于 Windows 操作系统的组件是不透明的。

 

IHV 为每个 VF 配置块分配一个唯一标识符。 这允许 VF 微型端口驱动程序查询或设置特定 VF 配置块上的信息。

VF 微型端口驱动程序通过以下功能，在指定的 VF 配置块上启动读取或写入操作：

-   [**NdisMReadConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)，用于从指定的 VF 配置块读取数据。 当 VF 微型端口驱动程序调用此函数时，它指定要读取的数据的块标识符和长度。 驱动程序还会传递指向包含所请求数据的缓冲区的指针。

-   [**NdisMWriteConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)，它将数据写入指定的 VF 配置块。 当 VF 微型端口驱动程序调用此函数时，它指定要写入的数据的块标识符和长度。 驱动程序还传递指向要从中写入数据的缓冲区的指针。

PF 微型端口驱动程序通过以下方式管理对指定的 VF 配置块的访问：

-   当 VF 微型端口驱动程序调用 [**NdisMReadConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)时，NDIS)  (oid 发出对象标识符，将 [oid \_ SRIOV \_ \_ \_ \_](./oid-sriov-read-vf-config-block.md) 的方法请求发送到 PF 微型端口驱动程序。 此 OID 请求包含函数调用中由 VF 微型端口驱动程序传递的参数数据。

    当驱动程序完成 OID 请求时，PF 微型端口驱动程序将执行读取操作并返回所请求的数据。 完成 OID 请求后，NDIS 将从对 [**NdisMReadConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)的调用返回。

-   当 VF 微型端口驱动程序调用 [**NdisMWriteConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)时，NDIS 向 PF 小型端口驱动程序发出 [oid \_ SRIOV \_ 写入 \_ VF \_ CONFIG \_ 块](./oid-sriov-write-vf-config-block.md) 的 oid 方法请求。 此 OID 请求包含函数调用中由 VF 微型端口驱动程序传递的参数数据。

    PF 微型端口驱动程序执行写入操作并完成 OID 请求。 完成 OID 请求后，NDIS 将从对 [**NdisMWriteConfigBlock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismreadconfigblock)的调用返回。

下图显示了通过 SR-IOV backchannel 接口读取和写入 VF 配置块所涉及的过程。

![图像显示了在 vf 微型端口驱动程序、ndis 和 pf 微型端口驱动程序之间移动的各种配置块](images/sriov-vf-backchannel.png)

 

