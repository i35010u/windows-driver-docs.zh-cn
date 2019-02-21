---
title: 连接和文件控制块管理例程
description: 连接和文件控制块管理例程
ms.assetid: e56c0cba-7352-4964-b067-57bc90c7f911
keywords:
- 块 WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33b9241ada099d4a45015a829de53e679116eed5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534336"
---
# <a name="connection-and-file-control-block-management-routines"></a>连接和文件控制块管理例程


连接和文件控制块管理例程用于通过 RDBSS 管理结构用于表示连接和文件控制块。

RDBSS 提供用于连接和文件控制块管理网络微型重定向程序驱动程序可以使用下面的例程：

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554356" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554356)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>此例程分配、 初始化，并将新的 FCB 结构插入到正在其打开此 FCB 的 NET_ROOT 结构的内存中数据结构。 分配的结构 SRV_OPEN 和 FOBX 结构有空间。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554358" data-raw-source="[&lt;strong&gt;RxCreateNetFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554358)"><strong>RxCreateNetFobx</strong></a></p></td>
<td align="left"><p>此例程分配、 初始化，并将插入新的文件对象扩展 (FOBX) 结构。 网络微型-重定向程序应调用此例程的末尾创建 FOBX 成功创建操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554366" data-raw-source="[&lt;strong&gt;RxCreateNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554366)"><strong>RxCreateNetRoot</strong></a></p></td>
<td align="left"><p>此例程生成表示 NET_ROOT 结构和关联的设备对象上的网络名称表中插入名称的节点。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554370" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554370)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>此例程生成一个表示服务器调用上下文并将其插入到 RDBSS 维护的网络名表名称的节点。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554376" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554376)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>此例程分配、 初始化，并将新的 SRV_OPEN 结构插入到 RDBSS 所使用的内存中数据结构。 如果必须分配一个新的结构，它具有为 FOBX 结构的空间。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554380" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554380)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>此例程生成表示 V_NET_ROOT 结构和网络名称表中插入名称的节点。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554388" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554388)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>此例程递减引用计数在多个引用计数的数据结构的实例由 RDBSS。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554409" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554409)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>此例程会删除到共享的连接。 根据指定的强制级别关闭的连接上打开任何文件。 网络微型重定向可能选择使传输连接保持打开状态，出于性能原因，除非指定的选项以强制关闭连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554412" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554412)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>此例程完成给定的 FCB 结构。 调用方必须具有与此 FCB 相关联的 NET_ROOT 结构的排他锁。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554418" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554418)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>此例程完成给定的 FOBX 结构。 调用方必须具有与此 FOBX 相关联的 FCB 的排他锁。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554421" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554421)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>此例程完成给定的 NET_ROOT 结构。 调用方应具有与此 NET_ROOT 结构 （通过 SRV_CALL 结构） 关联的设备对象的 NetName 表的排他锁。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554426" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554426)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>此例程完成给定的 SRV_CALL 结构。 调用方应与此 SRV_CALL 结构关联的设备对象对 NetName 表具有对锁的独占访问权限。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554432" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554432)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>此例程完成给定的 SRV_OPEN 结构。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554450" data-raw-source="[&lt;strong&gt;RxFinalizeVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554450)"><strong>RxFinalizeVNetRoot</strong></a></p></td>
<td align="left"><p>此例程完成给定的 V_NET_ROOT 结构。 调用方必须具有与此 V_NET_ROOT 结构关联的设备对象的 NetName 表锁的独占访问权限。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554454" data-raw-source="[&lt;strong&gt;RxFinishFcbInitialization&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554454)"><strong>RxFinishFcbInitialization</strong></a></p></td>
<td align="left"><p>此例程用于通过网络微型重定向完成的创建操作成功完成后初始化 FCB。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554463" data-raw-source="[&lt;strong&gt;RxForceFinalizeAllVNetRoots&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554463)"><strong>RxForceFinalizeAllVNetRoots</strong></a></p></td>
<td align="left"><p>此例程强制完成所有与给定 NET_ROOT 结构相关联的 V_NET_ROOT 结构。 调用方必须具有与此 V_NET_ROOT 结构关联的设备对象的 NetName 表锁的独占访问权限。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554478" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554478)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>此例程 FCB 标头，使用锁来确保一致读取的 64 位值中获取文件大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554493" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554493)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>此例程将尝试推断出的文件类型 （目录或非目录） 从 RX_CONTEXT 结构中的字段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554511" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554511)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>此例程称为从网络微型重定向来枚举 FCB 的文件锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff554603" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554603)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>此例程递减引用计数以及最终确定 FCB。</p>
<p>Windows Server 2003 Service Pack 1 (SP1) 及更高版本，此例程才可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554608" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554608)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>此例程递减 FCB 的引用计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554627" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554627)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>此例程递增 FCB 的引用计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554688" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554688)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>此例程递增 RDBSS 所使用的引用计数的数据结构的多个实例上的引用计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554728" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554728)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>此例程设置与任何给定的服务器 （SRV_CALL 结构） 关联的域名。</p></td>
</tr>
</tbody>
</table>

 

请注意，大量的宏还定义提供周围的包装[ **RxReference** ](https://msdn.microsoft.com/library/windows/hardware/ff554688)并[ **RxDeference** ](https://msdn.microsoft.com/library/windows/hardware/ff554388)的例程调试。 有关这些宏的详细信息，请参阅[诊断和调试](diagnostics-and-debugging.md)。

 

 




