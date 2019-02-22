---
title: WDI 任务命令优先级和现有的状态
description: 当适配器处于特定状态时，新的命令可能会涉及到它可能会影响现有状态 （例如，会影响现有连接的扫描）。
ms.assetid: 11EE42BF-2C44-4601-B262-570E6D154151
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b2d485a38cd8f4718ed28bc031ead8ba6a35aa5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519585"
---
# <a name="wdi-task-command-priority-and-existing-state"></a>WDI 任务命令优先级和现有的状态


当适配器处于特定状态时，新的命令可能会涉及到它可能会影响现有状态 （例如，会影响现有连接的扫描）。 下表描述了如何新的命令应优先对适配器中的现有状态。 列说明了新的命令时提供服务的现有状态。

新命令现有状态连接质量 (EAP) 的优先级 1 P2P 侦听优先级 2 连接质量延迟 （媒体流式处理使用） 的优先级 3 现有连接的 （强制） 的优先级 4 扫描/P2P 发现重要 （延迟扫描） 暂停暂停限制扫描/P2P（非强制性） 的发现重要 （跳过扫描） 重要维护 （跳过扫描） 限制工作站连接，漫游，断开连接延迟连接暂停暂停限制 P2P 转启动、 转停止延迟连接暂停暂停限制 P2P 客户端连接、 断开连接延迟连接暂停暂停限制 P2P 发送操作响应暂停暂停暂停限制 P2P 发送操作请求延迟发送保持暂停限制
 

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
<td align="left"><p>确定优先级高于新请求的现有状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>维护</p></td>
<td align="left"><p>同等优先级的现有状态与新的命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Throttle</p></td>
<td align="left"><p>减少维护的现有状态，以便它的工作原理，但设置优先级更高版本的新命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>暂停</p></td>
<td align="left"><p>停止处理现有的状态并尝试尽可能快地完成现有状态。</p></td>
</tr>
</tbody>
</table>

 

 

 





