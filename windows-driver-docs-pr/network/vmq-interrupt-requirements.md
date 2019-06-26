---
title: VMQ 中断要求
description: VMQ 中断要求
ms.assetid: 7ECC9031-D41B-4664-963D-F1C20B297B7C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b74301b77abf9a07db2a31d6c62925f96ac1a49f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376404"
---
# <a name="vmq-interrupt-requirements"></a>VMQ 中断要求


支持虚拟机队列 (VMQ) 功能的微型端口驱动程序还必须支持以下中断分配要求：

-   微型端口驱动程序必须支持 MSI X。 该驱动程序必须设置**NDIS\_接收\_筛选器\_MSI\_X\_支持**标志中**SupportedQueueProperties**成员[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

    驱动程序将返回在此结构[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构对其调用中使用该驱动程序[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数。

-   微型端口驱动程序必须调用[ **NdisGetRssProcessorInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetrssprocessorinformation)函数可获得分配中断向量的处理器信息。 它必须不依赖于注册表项或从中断分配其他源获取的信息。

    [**NdisGetRssProcessorInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisgetrssprocessorinformation)返回信息的微型端口驱动程序可以使用适用于 RSS 和 VMQ 处理器的集。 此信息包含在[ **NDIS\_RSS\_处理器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_rss_processor_info)结构。

-   微型端口驱动程序应为每个处理器中指定的分配仅一个中断向量[ **NDIS\_RSS\_处理器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_rss_processor_info)结构。

    微型端口驱动程序应为不发送或接收数据包的操作相关的其他事件分配不能超过两个中断向量。 例如，驱动程序分配 IDT 链接状态事件。

-   微型端口驱动程序必须支持 MSI X 中断向量下表中定义的最小数目：

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">队列数</th>
    <th align="left">所需的 MSI X 中断向量的最小数目</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>1–16</p></td>
    <td align="left"><p>1–16</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>17–64</p></td>
    <td align="left"><p>16–32</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>65 或更多</p></td>
    <td align="left"><p>32 或多个</p></td>
    </tr>
    </tbody>
    </table>

     

 

 





