---
title: VMQ 中断要求
description: VMQ 中断要求
ms.assetid: 7ECC9031-D41B-4664-963D-F1C20B297B7C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d7e461b18cc53dbc7637815bd52b24b0f8cb8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842946"
---
# <a name="vmq-interrupt-requirements"></a>VMQ 中断要求


支持虚拟机队列（VMQ）功能的微型端口驱动程序还必须支持以下中断分配要求：

-   微型端口驱动程序必须支持 MSI-X。 驱动程序必须将**ndis\_接收\_筛选器\_MSI\_X\_支持** **的标志**设置为[**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)构造.

    驱动程序在[**NDIS\_微型端口\_适配器中返回此结构\_硬件\_协助**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)驱动程序在其对[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的调用中使用的\_属性结构。

-   微型端口驱动程序必须调用[**NdisGetRssProcessorInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation)函数以获取用于分配中断向量的处理器信息。 它不得依赖注册表项或从其他源获取的用于中断分配的信息。

    [**NdisGetRssProcessorInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation)返回有关微型端口驱动程序可用于 RSS 和 VMQ 的处理器集的信息。 此信息包含在[**NDIS\_RSS\_PROCESSOR\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)结构。

-   小型端口驱动程序应该只为[**NDIS\_RSS\_processor\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)结构中指定的每个处理器分配一个中断向量。

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

     

 

 





