---
title: Bug 检查 0x3F NO_MORE_SYSTEM_PTES
description: NO_MORE_SYSTEM_PTES bug 检查具有 0x0000003F 值。 这是系统的执行了过多的 I/O 操作的结果。
ms.assetid: b8164ec3-87c3-4629-ab70-6addbf368b76
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
ms.openlocfilehash: 5efcfcccf46469af2dc73c43615b69d1c9d180c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361873"
---
# <a name="bug-check-0x3f-nomoresystemptes"></a>Bug 检查 0x3F：否\_更多\_系统\_PTE


否\_更多\_系统\_PTE bug 检查的值为 0x0000003F。 这是系统的执行了过多的 I/O 操作的结果。 这会导致零碎的系统页表项 (PTE)。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="nomoresystemptes-parameters"></a>否\_更多\_系统\_PTE 参数


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
<td align="left"><p><strong>0:</strong>系统扩展 PTE 类型</p>
<p><strong>1:</strong>非分页缓冲的池扩展 PTE 类型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>内存请求的大小</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>总可用的系统 Pte</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>总系统 Pte</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

在几乎所有情况下，系统不是实际 Pte 带。 相反，驱动程序已请求大块的内存，但没有连续块的大小足以满足此请求。

通常视频驱动程序将分配内核必须在成功完成的内存的量大。 某些备份程序执行相同的操作。

<a name="resolution"></a>分辨率
----------

**可能解决方法：** 修改注册表以增加系统 Pte 的总数。 如果这没有帮助，删除最近安装的任何软件，尤其是备份实用程序或占用大量磁盘的应用程序。

**调试问题：** 下面的方法可以用于调试 bug 检查 0x3F。

首先，获取堆栈跟踪，并使用[ **！ sysptes 3** ](-sysptes.md)扩展命令。

然后设置**HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\会话管理器\\内存管理\\TrackPtes**等于 dword 值 1，并重新启动。 这将导致系统以保存的堆栈跟踪。

这样，您可以显示有关 PTE 所有者的更多详细的信息。 例如：

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

如果系统用完 Pte 阅读文章**TrackPtes**已设置注册表值， [ **bug 检查 0xD8** ](bug-check-0xd8--driver-used-excessive-ptes.md) (驱动程序\_用于\_过量\_PTE) 而不是 0x3F，将发出。 这会导致此错误的驱动程序的名称将还显示。

 

 




