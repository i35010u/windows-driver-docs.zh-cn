---
title: 流式处理状态
description: 流式处理状态
ms.assetid: 1030e5cd-441b-4f6a-8f6a-21ce11aaca96
keywords:
- WDK AVStream 的视频捕获，流状态
- 捕获视频 WDK AVStream，流式传输状态
- 流状态 WDK 视频捕获
- 指出 WDK 视频捕获
- 停止状态 WDK 视频捕获
- 获取 WDK 视频捕获状态
- WDK 视频捕获的暂停状态
- 运行状态 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a1068fdabfc1dc1747065eb09693d4ab6a0db3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390864"
---
# <a name="streaming-states"></a>流式处理状态


每个流提供的微型驱动程序存在问题的四种状态之一：KSSTATE\_停止、 KSSTATE\_采集、 KSSTATE\_暂停或 KSSTATE\_运行。 在初始化时该流位于，默认情况下**KSSTATE\_停止**状态。 Stream 类接口发送时，将转换为其他状态所做[ **SRB\_设置\_流\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff568210)微型驱动程序的请求。 下表标识并描述了四个流状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSSTATE_STOP</p></td>
<td><p>当停止流状态时，微型驱动程序使用的资源，绝对最小值和微型驱动程序的队列中没有未完成数据 Srb。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_ACQUIRE</p></td>
<td><p>流状态正在获取资源，微型驱动程序会分配所有所需的资源，如 USB 和 IEEE 1394 上的带宽。</p></td>
</tr>
<tr class="odd">
<td><p>KSSTATE_PAUSE</p></td>
<td><p>流状态已暂停，微型驱动程序时，准备好立即对 KSSTATE_RUN 进行转换。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_RUN</p></td>
<td><p>微型驱动程序时流流状态，填充缓冲区并完成使用 Srb <strong>CompleteStreamSRB</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

 




