---
title: 流式处理状态
description: 流式处理状态
keywords:
- 视频捕获 WDK AVStream，流状态
- 捕获视频 WDK AVStream，流状态
- 流状态 WDK 视频捕获
- 状态 WDK 视频捕获
- 停止状态 WDK 视频捕获
- 获取状态 WDK 视频捕获
- 暂停状态 WDK 视频捕获
- 运行状态 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcedfcaaf4e658e3dd5cf37a955faaebc805df74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809831"
---
# <a name="streaming-states"></a>流式处理状态


微型驱动程序提供的每个流都存在以下四种状态之一： KSSTATE \_ 停止、KSSTATE \_ 获取、KSSTATE \_ 暂停或 KSSTATE \_ 运行。 初始化时，默认情况下，流处于 **KSSTATE \_ 停止** 状态。 当 Stream 类接口向微型驱动程序发送 [**SRB \_ 集 \_ 流 \_ 状态**](./srb-set-stream-state.md) 请求时，将转换为其他状态。 下表标识并描述四种流状态。

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
<td><p>当流状态为 "已停止" 时，微型驱动程序使用资源的绝对最小值，且微型驱动程序的队列中没有未完成的数据 SRBs。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_ACQUIRE</p></td>
<td><p>当流状态正在获取资源时，微型驱动程序将分配所需的所有资源，例如 USB 上的带宽和 IEEE 1394。</p></td>
</tr>
<tr class="odd">
<td><p>KSSTATE_PAUSE</p></td>
<td><p>当流状态为 "已暂停" 时，微型驱动程序准备好立即转换为 KSSTATE_RUN。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_RUN</p></td>
<td><p>流状态为流式处理时，微型驱动程序将使用 <strong>CompleteStreamSRB</strong>填充缓冲区并完成 SRBs。</p></td>
</tr>
</tbody>
</table>

 

 

