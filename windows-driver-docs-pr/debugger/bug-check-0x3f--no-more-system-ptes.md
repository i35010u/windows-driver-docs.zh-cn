---
title: Bug 检查 0x3F NO_MORE_SYSTEM_PTES
description: NO_MORE_SYSTEM_PTES bug 检查的值为0x0000003F。 这是系统执行过多 i/o 操作的结果。
keywords:
- Bug 检查 0x3F NO_MORE_SYSTEM_PTES
- NO_MORE_SYSTEM_PTES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NO_MORE_SYSTEM_PTES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4f84ed612905c0d3aff5d1f45331a9bf653d3482
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811215"
---
# <a name="bug-check-0x3f-no_more_system_ptes"></a>Bug 检查0x3F：不再 \_ 有 \_ 系统 \_ pte


不再 \_ \_ \_ 有系统 pte 错误检查的值为0x0000003F。 这是系统执行过多 i/o 操作的结果。 这会导致 (PTE) 的系统页表项出现碎片。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="no_more_system_ptes-parameters"></a>无 \_ 更多 \_ 系统 \_ pte 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p><strong>0：</strong> 系统扩展 PTE 类型</p>
<p><strong>1：</strong> 非分页池扩展 PTE 类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>内存请求大小</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>可用系统 Pte 总数</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>系统 Pte 总数</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

几乎在所有情况下，系统实际上不会有 Pte。 相反，驱动程序请求的内存块很大，但没有足够大的连续块来满足此请求。

通常，视频驱动程序会分配大量必须成功的内核内存。 某些备份程序会执行相同的操作。

<a name="resolution"></a>解决方法
----------

**可能的解决方法：** 修改注册表以增加系统 Pte 的总数。 如果这没有帮助，请删除所有最近安装的软件，尤其是备份实用工具或磁盘密集型应用程序。

**调试问题：** 以下方法可用于调试 bug 检查0x3F。

首先，获取堆栈跟踪，然后使用 [**！ sysptes 3**](-sysptes.md) extension 命令。

然后，设置 **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 控制 \\ 会话管理器的 \\ 内存管理 \\ TrackPtes** 等于 DWORD 1，然后重新启动。 这将导致系统保存堆栈跟踪。

这允许您显示有关 PTE 所有者的更详细信息。 例如：

```dbgcmd
0: kd> !sysptes 4

0x2c47 System PTEs allocated to mapping locked pages

VA       MDL     PageCount  Caller/CallersCaller
f0e5db48 eb6ceef0        1 ntkrpamp!MmMapLockedPages+0x15/ntkrpamp!IopfCallDriver+0x35
f0c3fe48 eb634bf0        1 netbt!NbtTdiAssociateConnection+0x1f/netbt!DelayedNbtProcessConnect+0x17c
f0db38e8 eb65b880        1 mrxsmb!SmbMmAllocateSessionEntry+0x89/mrxsmb!SmbCepInitializeExchange+0xda
f8312568 eb6df880        1 rdbss!RxCreateFromNetRoot+0x3d7/rdbss!RxCreateFromNetRoot+0x93
f8363908 eb685880        1 mrxsmb!SmbMmAllocateSessionEntry+0x89/mrxsmb!SmbCepInitializeExchange+0xda
f0c54248 eb640880        1 rdbss!RxCreateFromNetRoot+0x3d7/rdbss!RxCreateFromNetRoot+0x93
f0ddf448 eb5f3160        1 mrxsmb!MrxSmbUnalignedDirEntryCopyTail+0x387/mrxsmb!MRxSmbCoreInformation+0x36
f150bc08 eb6367b0        1 mrxsmb!MrxSmbUnalignedDirEntryCopyTail+0x387/mrxsmb!MRxSmbCoreInformation+0x36
f1392308 eb6fba70        1 netbt!NbtTdiOpenAddress+0x1fb/netbt!DelayedNbtProcessConnect+0x17c
eb1bee64 edac5000      200 VIDEOPRT!pVideoPortGetDeviceBase+0x118/VIDEOPRT!VideoPortMapMemory+0x45
f139b5a8 edd4b000       12 rdbss!FsRtlCopyWrite2+0x34/rdbss!RxDriverEntry+0x149
eb41f400 ede92000       20 VIDEOPRT!pVideoPortGetDeviceBase+0x139/VIDEOPRT!VideoPortGetDeviceBase+0x1b
eb41f198 edf2a000       20 NDIS!NdisReadNetworkAddress+0x3a/NDIS!NdisFreeSharedMemory+0x58
eb41f1e4 eb110000       10 VIDEOPRT!pVideoPortGetDeviceBase+0x139/VIDEOPRT!VideoPortGetDeviceBase+0x1b
......
```

如果在设置了 **TrackPtes** 注册表值之后系统再次运行了 pte，则会发出 [**bug 检查 0XD8**](bug-check-0xd8--driver-used-excessive-ptes.md) (驱动程序 \_ 使用 \_ 过多 \_ pte) ，而不是0x3F。 还将显示导致此错误的驱动程序的名称。

 

 




