---
title: VMQ 中断要求
description: VMQ 中断要求
ms.assetid: 7ECC9031-D41B-4664-963D-F1C20B297B7C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7230021daa6b10cbc4599c22fe86d9d165ff449
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543026"
---
# <a name="vmq-interrupt-requirements"></a>VMQ 中断要求


支持虚拟机队列 (VMQ) 功能的微型端口驱动程序还必须支持以下中断分配要求：

-   微型端口驱动程序必须支持 MSI X。 该驱动程序必须设置**NDIS\_接收\_筛选器\_MSI\_X\_支持**标志中**SupportedQueueProperties**成员[ **NDIS\_接收\_筛选器\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566864)结构。

    驱动程序将返回在此结构[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构对其调用中使用该驱动程序[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数。

-   微型端口驱动程序必须调用[ **NdisGetRssProcessorInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff562669)函数可获得分配中断向量的处理器信息。 它必须不依赖于注册表项或从中断分配其他源获取的信息。

    [**NdisGetRssProcessorInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff562669)返回信息的微型端口驱动程序可以使用适用于 RSS 和 VMQ 处理器的集。 此信息包含在[ **NDIS\_RSS\_处理器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567274)结构。

-   微型端口驱动程序应为每个处理器中指定的分配仅一个中断向量[ **NDIS\_RSS\_处理器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567274)结构。

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

     

 

 





