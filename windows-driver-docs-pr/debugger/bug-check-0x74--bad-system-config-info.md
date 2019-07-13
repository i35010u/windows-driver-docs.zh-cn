---
title: Bug 检查 0x74 BAD_SYSTEM_CONFIG_INFO
description: BAD_SYSTEM_CONFIG_INFO bug 检查具有 0x00000074 值。 检查此错误指示在注册表中存在错误。
ms.assetid: c59ddc44-d860-4fbb-a975-ae7226fdce86
keywords:
- Bug 检查 0x74 BAD_SYSTEM_CONFIG_INFO
- BAD_SYSTEM_CONFIG_INFO
ms.date: 03/24/2019
topic_type:
- apiref
api_name:
- BAD_SYSTEM_CONFIG_INFO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 837a976c122fc1f49a06186b47b80c8cd9724b20
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866526"
---
# <a name="bug-check-0x74-badsystemconfiginfo"></a>Bug 检查 0x74：错误\_系统\_CONFIG\_信息

缺点\_系统\_CONFIG\_信息错误检查的值为 0x00000074。 检查此错误指示在注册表中存在错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="badsystemconfiginfo-parameters"></a>错误\_系统\_CONFIG\_信息参数


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
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>NT 状态值/代码 （如果可用）</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

缺点\_系统\_CONFIG\_如果系统配置单元已损坏，则会出现信息 bug 检查。 但是，这种损坏，不太可能，因为引导加载程序，在加载配置单元时检查已损坏的 hive。

如果是缺少一些关键的注册表项和值，也可能发生此错误检查。 如果手动编辑注册表，用户或应用程序或服务损坏注册表，键和值可能会丢失。

查找参数 4 中返回的 NT 状态值可以提供其他信息，请参阅[NTSTATUS 值](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)有关的列表。 

<a name="resolution"></a>分辨率
----------

若要查看是否有任何注册表的 Windows 系统事件日志中检查相关错误事件。 如果，看到如果此事件将列出 hive 或中发生错误的特定键。

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

```dbgcmd
BAD_SYSTEM_CONFIG_INFO (74)
Can indicate that the SYSTEM hive loaded by the osloader/NTLDR
was corrupt.  This is unlikely, since the osloader will check
a hive to make sure it isn't corrupt after loading it.
It can also indicate that some critical registry keys and values
are not present.  (i.e. somebody used regedt32 to delete something
that they shouldn't have)  Booting from LastKnownGood may fix
the problem, but if someone is persistent enough in mucking with
the registry they will need to reinstall or use the Emergency
Repair Disk.
Arguments:
Arg1: 0000000000000002, (reserved)
Arg2: ffffd481054b49f0, (reserved)
Arg3: 0000000000000004, (reserved)
Arg4: ffffffffc000014c, usually the NT status code.

```

查看所有返回的信息 ！ 若要了解有关失败的分析。

使用[！ 错误](-error.md)扩展名，即可显示参数 4 中的 NTSTATUS 值有关的信息。

```dbgcmd
2: kd> !ERROR ffffffffc000014c
Error code: (NTSTATUS) 0xc000014c (3221225804) - {The Registry Is Corrupt}  The structure of one of the files that contains Registry data is corrupt, or the image of the file in memory is corrupt, or the file could not be recovered because the alternate copy or log was absent or corrupt.
```

使用[！ reg](-reg.md)扩展名以显示有关注册表配置单元提供示例，在注册表中的信息。

```dbgcmd
!reg hivelist

-------------------------------------------------------------------------------------------------------------------------------------------------------
|     HiveAddr     |Stable Length|    Stable Map    |Volatile Length|    Volatile Map    |MappedViews|PinnedViews|U(Cnt)|     BaseBlock     | FileName 
-------------------------------------------------------------------------------------------------------------------------------------------------------
| ffff95077ea24000 |       1000  | ffff95077ea24588 |          0    |  0000000000000000  |     0| ffff95077ea31000  | <NONAME>
| ffff95077ea3e000 |    12d3000  | ffff95077ea49000 |      21000    |  ffff95077ea3e800  |     0| ffff95077ea40000  | SYSTEM
| ffff95077ea8f000 |      53000  | ffff95077ea8f588 |       9000    |  ffff95077ea8f800  |     0| ffff95077ea91000  | <NONAME>
| ffff9507821c8000 |       7000  | ffff9507821c8588 |          0    |  0000000000000000  |     0| ffff9507821cc000  | kVolume2\EFI\Microsoft\Boot\BCD
| ffff95077f6ae000 |    685c000  | ffff95077f737000 |       6000    |  ffff95077f6ae800  |     0| ffff95077f6b6000  | emRoot\System32\Config\SOFTWARE
-------------------------------------------------------------------------------------------------------------------------------------------------------
```

使用 ！ reg openkeys 命令以查看哪个注册表项已打开。

```dbgcmd
2: kd> !reg openkeys

Hive: \REGISTRY\MACHINE\SYSTEM
===========================================================================================
Index 0:     00000000 kcb=ffffd805e303c728 cell=00000020 f=002c0100 \REGISTRY\MACHINE\SYSTEM
Index 1:     db67f96d kcb=ffffd805e416ed18 cell=00bd0b40 f=00200080 \REGISTRY\MACHINE\SYSTEM\WPA\8DEC0AF1-0341-4B93-85CD-72606C2DF94C-7P-374
Index 3:     db67ee93 kcb=ffffd805e30c5ab8 cell=00bc1550 f=00200080 \REGISTRY\MACHINE\SYSTEM\WPA\8DEC0AF1-0341-4B93-85CD-72606C2DF94C-7P-161
Index 4:     f9909d96 kcb=ffffd805e44bd268 cell=00bf8f50 f=00200000 \REGISTRY\MACHINE\SYSTEM\CONTROLSET001\CONTROL\POWER\PROFILE\EVENTS\{54533251-82BE-4824-96C1-47B60B740D00}\{8BC6262C-C026-411D-AE3B-7E2F70811A13}
Index 5:     e9dd6ce5 kcb=ffffd805e4180e48 cell=00812970 f=00200000 \REGISTRY\MACHINE\SYSTEM\DRIVERDATABASE

...

```


**时间的差旅跟踪**

如果可以按要求重现 bug 检查，调查花些时间旅行跟踪使用 WinDbg 预览的可能性。 有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。

<a name="remarks"></a>备注
----------

尝试进入安全模式启动，然后正常重新启动操作系统。 如果在重新启动无法解决问题，是太多，注册表损坏。 请尝试以下步骤。

- 如果您的系统还原点，请尝试还原到早期的还原点。
- 重置您的 PC。
- 使用安装媒体还原或重置您的 PC。
- 使用安装媒体重新安装 Windows。

有关详细信息，请参阅[Windows 10 中的恢复选项](https://support.microsoft.com/help/12415/windows-10-recovery-options#)。

支持本文讨论了此 bug 检查代码：[错误 0x74:Bad_system_config_info](https://support.microsoft.com/help/4028653/windows-error-0x74-badsystemconfiginfo)
