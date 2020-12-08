---
title: 修改 IEEE 1394 总线驱动程序的默认行为
description: Windows 7 包括 1394ohci.sys，这是通过使用内核模式驱动程序框架（ (KMDF) 实现的新 IEEE 1394 总线驱动程序）。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8734d411d5c366e0ba1516653d3f197d3fb1e160
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798209"
---
# <a name="modifying-the-default-behavior-of-the-ieee-1394-bus-driver"></a>修改 IEEE 1394 总线驱动程序的默认行为


Windows 7 包括 1394ohci.sys，这是通过使用内核模式驱动程序框架（ (KMDF) 实现的新 IEEE 1394 总线驱动程序）。 1394ohci.sys 总线驱动程序替换端口/微型端口配置中的旧版 IEEE bus 驱动程序--1394bus.sys 和 ochi1394.sys。

在某些情况下，你可能想要重写 1394ohci.sys 的默认行为。 为此，可以设置它所支持的特定注册表值。

## <a name="registry-value-locations"></a>注册表值位置


你可以为系统中的所有1394控制器全局设置1394相关的注册表值，也可以为每个1394控制器分别设置。 1394ohci.sys 总线驱动程序首先查询全局1394注册表值，然后查询各个1394控制器注册表值。

以下注册表位置包含全局1394注册表值：

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\1394ohci \Parameters`

以下注册表位置包含各个1394控制器注册表值：

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class \{6BDD1FC1-810F-11D0-BEC7-08002BE2092F}\<NNNN>`

`<NNNN>` 表示每个1394控制器的实例标识号。

## <a name="registry-values"></a>注册表值


下表介绍了新的1394总线驱动程序支持的注册表值。 可以为特定1394控制器指定全局或全部注册表值。 为特定1394控制器指定的任何注册表值都将覆盖所有对应的全局指定的注册表值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>类型</th>
<th>值</th>
<th>默认</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>DisableGenerationCountCompare</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>0</td>
<td>1394ohci.sys 总线驱动程序将1394控制器的 <strong>self_id</strong> 寄存器中的生成计数值与异步接收 DMA 请求上下文缓冲区在处理收到的异步请求时接收的生成计数值进行比较。 如果将此值设置为0，则启用生成计数比较。 将此值设置为1将禁用生成计数比较。</td>
</tr>
<tr class="even">
<td>UseQuadletReadsForEnumeration</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>0</td>
<td>如果将此值设置为0，则将启用用于检索配置 ROM 内容的默认方法。 将此值设置为1会导致新的1394总线驱动程序使用异步 quadlet 读取事务来检索配置 ROM 的内容。</td>
</tr>
<tr class="odd">
<td>EnumerateIP1394</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>0</td>
<td>如果将此值设置为0，则将在1394总线上禁用 IP1394 设备的枚举。 将此值设置为1可在1394总线上枚举 IP1394 设备。</td>
</tr>
<tr class="even">
<td>EnableGapCountOptimization</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>仅针对1394a 拓扑优化</td>
<td>将此值设置为0将禁用间隙计数优化。 将此值设置为1可启用间隙计数优化。
<div class="alert">
<strong>注意</strong>  启用间隙计数优化可改进所有1394总线拓扑（包括1394b）的间隙计数。 根据 IEEE-1394a 规范中指定的表方法，使用的 "间隙计数" 值。 最终用户必须确保使用的间距计数对其1394总线拓扑有效。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>EnablePersistentCycleStarts</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>0</td>
<td>如果在1394总线上找不到支持同步的节点，则将此值设置为0将禁用循环启动数据包。 将此值设置为1可启用循环启动数据包，无论是否在1394总线上都找到了支持同步的节点。
<div class="alert">
<strong>注意</strong>  1394ohci.sys 总线驱动程序将禁用，并且仅当本地节点为总线管理器时，才启用循环启动数据包。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[IEEE 1394 驱动程序堆栈](./the-ieee-1394-driver-stack.md)  
[Windows 7 中的 IEEE 1394 总线驱动程序](./ieee-1394-bus-driver-in-windows-7.md)
