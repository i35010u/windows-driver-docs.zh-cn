---
title: WDI 任务命令优先级和现有状态
description: 当适配器处于某一特定状态时，可能会出现新的命令，该命令可能会影响现有状态 (例如，影响现有连接的扫描) 。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c544f4ad831af149761e276a390b86f405d51ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822061"
---
# <a name="wdi-task-command-priority-and-existing-state"></a>WDI 任务命令优先级和现有状态


当适配器处于某一特定状态时，可能会出现新的命令，该命令可能会影响现有状态 (例如，影响现有连接的扫描) 。 下表描述了如何根据适配器中的现有状态确定新命令的优先级。 这些列描述了在新命令进入时如何为现有状态提供服务。

新命令 (EAP) 的状态连接质量 EAP 优先级为1的 P2P 侦听优先级2连接质量延迟 (媒体流式处理) -优先级3现有连接-优先级4扫描/P2P 发现 (强制) 重要 (延迟扫描) 暂停暂停中止扫描/P2P 发现 (不强制执行跳过扫描) 限制站连接漫游、断开连接延迟连接暂停暂停阻止 P2P 开始、停止延迟连接暂停暂停阻止 P2P 客户端连接、断开延迟连接暂停暂停阻止 P2P 发送操作响应暂停暂停暂停阻止 P2P 发送操作请求延迟发送保持暂停中止
 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>重要</p></td>
<td align="left"><p>将现有状态设置为高于新请求的优先级。</p></td>
</tr>
<tr class="even">
<td align="left"><p>维护</p></td>
<td align="left"><p>将现有状态和新命令的优先级相等。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>限制</p></td>
<td align="left"><p>阻止现有状态的维护，以使其正常工作，但使新命令的优先级更高。</p></td>
</tr>
<tr class="even">
<td align="left"><p>暂停</p></td>
<td align="left"><p>停止服务现有状态并尝试尽快完成现有状态。</p></td>
</tr>
</tbody>
</table>

 

 

 





