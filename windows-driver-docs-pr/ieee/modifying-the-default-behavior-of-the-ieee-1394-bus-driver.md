---
title: 修改 IEEE 1394 总线驱动程序的默认行为
description: Windows 7 包括 1394ohci.sys，新的 IEEE 1394 总线驱动程序使用内核模式驱动程序框架 (KMDF) 实现的。
ms.assetid: B636943E-EE52-4D0D-A638-89C05AD41F1A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 305c180c8c9930b43a420d72395a4bdc2ffc9bf0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564106"
---
# <a name="modifying-the-default-behavior-of-the-ieee-1394-bus-driver"></a>修改 IEEE 1394 总线驱动程序的默认行为


Windows 7 包括 1394ohci.sys，新的 IEEE 1394 总线驱动程序使用内核模式驱动程序框架 (KMDF) 实现的。 1394ohci.sys 总线驱动程序将替换中端口/微型端口配置-1394bus.sys 和 ochi1394.sys 的旧 IEEE 总线驱动程序。

在某些情况下你可能想要重写 1394ohci.sys 的默认行为。 可以通过设置它支持某些注册表值来执行此操作。

## <a name="registry-value-locations"></a>注册表值位置


可以针对所有的 1394 年控制器的全局系统中或单独为每个 1394年控制器来设置 1394年相关的注册表值。 1394ohci.sys，总线驱动程序首先查询全局 1394年注册表值，然后查询各个 1394年控制器注册表值。

在以下注册表位置包含全局 1394年注册表值：

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\1394ohci \Parameters`

在以下注册表位置包含各个 1394年控制器注册表值：

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class \{6BDD1FC1-810F-11D0-BEC7-08002BE2092F}\<NNNN>`

`<NNNN>` 表示每个 1394年控制器的实例标识号。

## <a name="registry-values"></a>注册表值


下表介绍新的 1394年总线驱动程序支持的注册表值。 全局或为特定的 1394年控制器，可以指定所有注册表值。 为特定的 1394年控制器指定的任何注册表值重写任何对应的全局指定的注册表值。

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
<th>在任务栏的搜索框中键入</th>
<th>ReplTest1</th>
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
<td>1394ohci.sys 总线驱动程序中的生成计数值进行比较<strong>self_id</strong>注册 1394年控制器与中的异步接收的生成计数值的处理时接收 DMA 请求上下文缓冲区接收异步请求。 将此值设置为 0 允许生成计数比较。 此值设置为 1 禁用生成计数比较。</td>
</tr>
<tr class="even">
<td>UseQuadletReadsForEnumeration</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>0</td>
<td>设置此值为 0，用于检索配置 rom。 内容的默认方法 此值设置为 1 会导致新的 1394年总线驱动程序，使用异步 quadlet 读取的事务来检索内容配置 rom。</td>
</tr>
<tr class="odd">
<td>EnumerateIP1394</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>0</td>
<td>将此值设置为 0 将禁用 1394年总线上 IP1394 设备的枚举。 此值设置为 1 启用 1394年总线上 IP1394 设备的枚举。</td>
</tr>
<tr class="even">
<td>EnableGapCountOptimization</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>优化为仅限 1394a 拓扑</td>
<td>将此值设置为 0 会禁用间隙计数优化。 此值设置为 1 可实现间隙计数优化。
<div class="alert">
<strong>请注意</strong>  启用间隙计数优化改进了所有的 1394年总线拓扑，包括 1394b 的间隔计数。 使用的间隔计数值基于 IEEE 1394a 规范中指定的表方法。 最终用户必须确保使用的间隔计数是对其的 1394年总线拓扑有效。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td>EnablePersistentCycleStarts</td>
<td>DWORD</td>
<td>0 或 1</td>
<td>0</td>
<td>如果没有等时支持的节点上的 1394年总线发现，此值设置为 0 禁用周期开始数据包。 此值设置为 1 启用周期开始数据包而不考虑是否 1394年总线上找到等时支持的节点。
<div class="alert">
<strong>请注意</strong>  1394ohci.sys 总线驱动程序禁用和启用周期开始数据包，仅当本地节点是总线管理器。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[IEEE 1394 驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/ff538867)  
[在 Windows 7 中的 IEEE 1394 总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/gg266402)  



