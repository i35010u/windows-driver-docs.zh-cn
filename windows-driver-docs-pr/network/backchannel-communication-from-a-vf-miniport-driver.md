---
title: Backchannel 通信从 VF 微型端口驱动程序
description: Backchannel 通信从 VF 微型端口驱动程序
ms.assetid: B7208199-1308-4EF1-A03B-237A283563C4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f44ff7d450ea1cfb64c6727c1afc0cc63486b0b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546635"
---
# <a name="backchannel-communication-from-a-vf-miniport-driver"></a>Backchannel 通信从 VF 微型端口驱动程序


微型端口驱动程序的 PCI Express (PCIe) 虚拟函数 (VF) 与微型端口驱动程序的 PCIe 物理函数 (PF) 来读取或写入数据从 VF 配置块进行通信。

VF 配置块用于 backchannel PF 和 VF 微型端口驱动程序之间的通信。 独立硬件供应商 (IHV) 可以定义一个或多个 VF 配置块设备。 每个 VF 配置块都有 IHV 定义的格式、 长度和块 id。 例如，IHV 可以定义可用于 VF 微型端口驱动程序的媒体访问控制 (MAC) 地址 VF 配置块。 另一个 VF 配置块可用于当前 VF 和虚拟端口 (VPort) 配置。

**请注意**  仅由 PF 和 VF 微型端口驱动程序使用每个 VF 配置块中的数据。 格式和内容的此数据是不透明的 Windows 操作系统组件。

 

每个 VF 配置块由 IHV 分配的唯一标识符。 这允许 VF 微型端口驱动程序来查询或特定 VF 配置块上设置的信息。

VF 微型端口驱动程序启动读取或写入操作对指定 VF 配置块通过以下函数：

-   [**NdisMReadConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)，其中从指定的 VF 配置块中读取数据。 当 VF 微型端口驱动程序调用此函数时，它指定的块标识符和要读取的数据长度。 该驱动程序还将指针传递给将包含所请求的数据的缓冲区。

-   [**NdisMWriteConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)，其中将数据写入到指定的 VF 配置块。 当 VF 微型端口驱动程序调用此函数时，它指定的块标识符和要写入的数据长度。 该驱动程序还将指针传递给要写入的数据缓冲区。

PF 微型端口驱动程序中通过以下方式管理对指定 VF 配置块的访问：

-   当 VF 微型端口驱动程序调用[ **NdisMReadConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)，NDIS 发出的一个对象标识符 (OID) 方法请求[OID\_SRIOV\_读取\_VF\_CONFIG\_阻止](https://msdn.microsoft.com/library/windows/hardware/hh451874)到 PF 微型端口驱动程序。 此 OID 请求包含由 VF 微型端口驱动程序函数调用中传递的参数数据。

    PF 微型端口驱动程序执行读取的操作，并返回所请求的数据时驱动程序完成 OID 请求。 OID 请求完成后，从调用返回 NDIS [ **NdisMReadConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)。

-   当 VF 微型端口驱动程序调用[ **NdisMWriteConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)，NDIS 颁发的 OID 方法请求[OID\_SRIOV\_编写\_VF\_CONFIG\_阻止](https://msdn.microsoft.com/library/windows/hardware/hh451918)到 PF 微型端口驱动程序。 此 OID 请求包含由 VF 微型端口驱动程序函数调用中传递的参数数据。

    PF 微型端口驱动程序执行写入操作，并完成 OID 请求。 OID 请求完成后，从调用返回 NDIS [ **NdisMWriteConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451523)。

下图显示过程所涉及到读取和写入通过 SR-IOV backchannel 接口 VF 配置块。

![图显示了各种配置块 vf 微型端口驱动程序、 ndis 和 pf 微型端口驱动程序之间移动](images/sriov-vf-backchannel.png)

 

 





