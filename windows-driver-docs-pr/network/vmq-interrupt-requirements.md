---
title: VMQ 中断要求
description: VMQ 中断要求
ms.assetid: 7ECC9031-D41B-4664-963D-F1C20B297B7C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c12f34507238eca0b6b0c2067f04d674b8b316b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216904"
---
# <a name="vmq-interrupt-requirements"></a>VMQ 中断要求


支持虚拟机队列 (VMQ) 功能的微型端口驱动程序还必须支持以下中断分配要求：

-   微型端口驱动程序必须支持 MSI-X。 驱动程序必须在[**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的**SupportedQueueProperties**成员中设置**ndis \_ 接收 \_ 筛选器 \_ MSI \_ X \_ 支持**的标志。

    驱动程序在 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构中返回此结构，驱动程序在其对 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数的调用中使用。

-   微型端口驱动程序必须调用 [**NdisGetRssProcessorInformation**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation) 函数以获取用于分配中断向量的处理器信息。 它不得依赖注册表项或从其他源获取的用于中断分配的信息。

    [**NdisGetRssProcessorInformation**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation) 返回有关微型端口驱动程序可用于 RSS 和 VMQ 的处理器集的信息。 此信息包含在 [**NDIS \_ RSS \_ 处理器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info) 结构中。

-   小型端口驱动程序应该只为 [**NDIS \_ RSS \_ 处理器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info) 结构中指定的每个处理器分配一个中断向量。

    小型端口驱动程序应为与发送或接收数据包操作无关的其他事件分配两个以上的中断向量。 例如，驱动程序可以为链接状态事件分配一个 IDT。

-   微型端口驱动程序必须支持下表中定义的最小 MSI-X 中断向量：

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">队列数</th>
    <th align="left">所需的 MSI-X 中断向量的最小数目</th>
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
    <td align="left"><p>65或更多</p></td>
    <td align="left"><p>32或更多</p></td>
    </tr>
    </tbody>
    </table>

     

 

