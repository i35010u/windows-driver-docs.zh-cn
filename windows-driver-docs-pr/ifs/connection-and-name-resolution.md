---
title: 连接和名称解析
description: 连接和名称解析
ms.assetid: e61d09f1-7951-4291-93ce-e5ccbe0be576
keywords:
- 最小重定向程序 WDK，连接
- 最小重定向程序 WDK、 名称解析
- 名称 WDK 文件系统
- 连接 WDK 微型-重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1948c4086bdfe5a7f8d6bb813e6a99a83f270e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568423"
---
# <a name="connection-and-name-resolution"></a>连接和名称解析


网络微型-重定向程序建立与远程服务器连接和处理使用多个例程的名称解析。 RDBSS 将此进程抽象化为多个结构包括 SRV\_调用时，NET\_根和 V\_NET\_根结构的引用计数。 在网络微型重定向术语中，建立连接通常称为"树连接。" 建立此连接需要创建 SRV\_调用、 NET\_根和 V\_NET\_根结构。 正常的过程不会对网络微型重定向的调用以便[ **MRxCreateSrvCall** ](https://msdn.microsoft.com/library/windows/hardware/ff549864)例程通过调用后接[ **MRxSrvCallWinnerNotify**](https://msdn.microsoft.com/library/windows/hardware/ff550824)并[ **MRxCreateVNetRoot** ](https://msdn.microsoft.com/library/windows/hardware/ff549869)例程。 这些调用通常来自要装载驱动器的用户模式应用程序或服务的请求响应中发出 (**使用 x:，net \\\\服务器\\公共**，例如)。 这些调用也可能来自 UNC 文件对象的请求 (**记事本\\\\服务器\\公共\\readme.txt**，例如)。 RDBSS 处理这两种情况在内部的网络微型重定向，并启动**MRxCreateSrvCall**序列。

连接时已删除，类似完成调用都是关闭 SRV\_调用时，并 NET\_根结构并释放任何内存使用。 网络微型重定向到这些调用包括[ **MRxFinalizeVNetRoot**](https://msdn.microsoft.com/library/windows/hardware/ff550663)， [ **MRxFinalizeNetRoot**](https://msdn.microsoft.com/library/windows/hardware/ff550653)，和[**MRxFinalizeSrvCall**](https://msdn.microsoft.com/library/windows/hardware/ff550656)。

RDBSS 的原始设计是各种网络微型重定向将共享的 RDBSS，单个副本，但没有实施此功能。 从该原始设计遗留是各种网络微型重定向争用来满足网络连接的请求 (\\\\server\\共享，例如)。 [ **MRxSrvCallWinnerNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff550824) RDBSS 使用例程，它是获胜者，当多个重定向程序无法完成请求时通知网络微型重定向。 入选网络的微型重定向需要创建 SRV\_调用并建立与服务器的连接。

下 RDBSS 在 Windows Server 2003、 Windows XP 和 Windows 2000 中实现时，每个网络微型重定向有其自己的 RDBSS 副本，因此在 RDBSS 层包含任何竞争的网络重定向程序。 每个网络微型重定向 （网络提供商） 以及其 RDBSS 的本地副本被称为反过来基于注册表设置中的顺序：在其中查询提供程序的顺序由以下注册表值控制：

```cpp
ProviderOrder
```

此注册表值位于以下注册表项下：

```cpp
HKLM\CurrentControlSet\Control\NetworkProvider\Order
```

[ **MRxSrvCallWinnerNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff550824)例程将在调用完每个请求创建 SRV\_调用结构。

下表列出了可以由网络微型重定向的连接和名称解析操作的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549864" data-raw-source="[&lt;strong&gt;MRxCreateSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549864)"><strong>MRxCreateSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向创建 SRV_CALL 结构并与服务器建立连接。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549869" data-raw-source="[&lt;strong&gt;MRxCreateVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549869)"><strong>MRxCreateVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向创建 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550649" data-raw-source="[&lt;strong&gt;MRxExtractNetRootName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550649)"><strong>MRxExtractNetRootName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向从给定的路径名称 NET_ROOT 结构提取的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550653" data-raw-source="[&lt;strong&gt;MRxFinalizeNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550653)"><strong>MRxFinalizeNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成 NET_ROOT 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550656" data-raw-source="[&lt;strong&gt;MRxFinalizeSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550656)"><strong>MRxFinalizeSrvCall</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成用于建立与服务器连接的 SRV_CALL 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550663" data-raw-source="[&lt;strong&gt;MRxFinalizeVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550663)"><strong>MRxFinalizeVNetRoot</strong></a></td>
<td align="left"><p>RDBSS 调用此例程以请求网络微型重定向完成 V_NET_ROOT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550750" data-raw-source="[&lt;strong&gt;MRxPreparseName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550750)"><strong>MRxPreparseName</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，以使网络微型重定向有机会 preparse 一个名称。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550824" data-raw-source="[&lt;strong&gt;MRxSrvCallWinnerNotify&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550824)"><strong>MRxSrvCallWinnerNotify</strong></a></td>
<td align="left"><p>此例程最初设计用于由 RDBSS 以通知网络微型重定向，它是获胜者，当多个重定向程序无法完成请求时调用。 入选网络的微型重定向需要创建 SRV_CALL 结构并建立与服务器的连接。</p>
<p>下 RDBSS 的当前实现每个网络微型重定向有其自己的 RDBSS，副本，因此在 RDBSS 层包含任何竞争的网络重定向程序。 此例程将在创建 SRV_CALL 结构的每个请求之前调用。</p>
<p>如果多个重定向程序安装为处理同一个 UNC 命名空间中，MUP 基于重定向程序在注册表中指定的顺序选择重定向程序若要为请求提供服务。</p></td>
</tr>
</tbody>
</table>

 

 

 




