---
title: Bug 检查 0x74 BAD_SYSTEM_CONFIG_INFO
description: BAD_SYSTEM_CONFIG_INFO bug 检查的值为0x00000074。 此错误检查表示注册表中存在错误。
keywords:
- Bug 检查 0x74 BAD_SYSTEM_CONFIG_INFO
- BAD_SYSTEM_CONFIG_INFO
ms.date: 01/29/2021
topic_type:
- apiref
api_name:
- BAD_SYSTEM_CONFIG_INFO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4b69b7238a2ff96992e4f6d4a2ce8484ac2f3fe
ms.sourcegitcommit: 91632914d86484a6ab6340b04c1ee2d92ff7cf09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2021
ms.locfileid: "99534277"
---
# <a name="bug-check-0x74-bad_system_config_info"></a>Bug 检查0x74：错误的 \_ 系统 \_ 配置 \_ 信息

错误的 \_ 系统 \_ 配置 \_ 信息错误检查的值为0x00000074。 此错误检查表示注册表中存在错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="bad_system_config_info-parameters"></a>错误的 \_ 系统 \_ 配置 \_ 信息参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>如果可用，则为 "NT 状态值/代码" () </p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

\_ \_ \_ 如果系统配置单元已损坏，则会发生错误的系统配置信息 bug 检查。 但是，这种损坏的可能性不大，因为启动加载程序会在加载 hive 时检查 hive 是否损坏。

如果缺少某些关键的注册表项和值，也会发生此 bug 检查。 如果用户手动编辑了注册表，或者应用程序或服务损坏了注册表，则可能缺少键和值。

查找参数4中返回的 NT status 值可提供其他信息，有关列表，请参阅 [NTSTATUS 值](/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55) 。 

<a name="resolution"></a>解决方法
----------

检查 Windows 系统事件日志，以查看是否存在任何与注册表相关的错误事件。 如果事件列出了该错误发生在中的 hive 或特定键，则为。

[!analyze](-analyze.md) 调试扩展显示有关 bug 检查的信息，并有助于确定根本原因  。

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

查看由！分析返回的所有信息，以了解有关失败的信息。

使用 [！ error](-error.md) 扩展显示有关参数4中的 NTSTATUS 值的信息。

```dbgcmd
2: kd> !ERROR ffffffffc000014c
Error code: (NTSTATUS) 0xc000014c (3221225804) - {The Registry Is Corrupt}  The structure of one of the files that contains Registry data is corrupt, or the image of the file in memory is corrupt, or the file could not be recovered because the alternate copy or log was absent or corrupt.
```

使用 [！ reg](-reg.md) extenstion 显示有关注册表的信息，例如注册表中存在的配置单元。

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

使用！ reg sys.openkeys 命令查看打开了哪些注册表项。

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

## <a name="remarks"></a>备注

有关确定蓝屏原因的一般信息，请参阅 [蓝色屏幕数据](blue-screen-data.md)。

最好确认是否有足够的硬盘驱动器或 SSD 存储可用于使操作系统正常运行。

系统文件检查器工具可查找 Windows 中的损坏。 有关详细信息，请参阅 [使用系统文件检查器工具修复丢失或损坏的系统文件](https://support.microsoft.com/topic/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system-files-79aa86cb-ca52-166a-92a3-966e85d4094e)。

尝试启动进入安全模式，然后正常重新启动操作系统。 如果重新启动不能解决问题，则注册表损坏情况太大。 请尝试以下步骤。

- 如果你有系统还原点，请尝试还原到较早的还原点。
- 重置你的电脑。
- 使用安装媒体还原或重置你的电脑。
- 使用安装媒体重新安装 Windows。

有关详细信息，请参阅 [Windows 10 中的恢复选项](https://support.microsoft.com/help/12415/windows-10-recovery-options#)。

此支持文章讨论了此错误检查代码： [错误0x74： Bad_system_config_info](https://support.microsoft.com/help/4028653/windows-error-0x74-badsystemconfiginfo)
