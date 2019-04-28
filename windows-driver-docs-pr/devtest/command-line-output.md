---
title: 命令行输出
description: 命令行输出
ms.assetid: 21225785-e8b8-4488-b0a0-fe4cea50d1ff
keywords:
- 输出文件 WDK Static Driver Verifier
- 命令行输出 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b0caf66d4f52e3c062f5f4d431e3fbd66d313f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343100"
---
# <a name="command-line-output"></a>命令行输出


提交到 SDV 命令，它会显示有关命令的信息，在执行，状态消息，以指示成功或失败的命令中，任何错误消息或可能已生成的警告。 输出的底部将显示的验证结果的摘要。

例如下, 图显示的命令来验证使用的 SDV FailDriver WDM 示例驱动程序的命令行输出[SpinLock](wdm-spinlock.md)规则。 SDV FailDriver WDM 示例驱动程序的驱动程序有有意编码错误，位于\\工具\\sdv\\示例\\Sdv FailDriver WDM 文件夹的 Windows 驱动程序示例。

在此验证，SDV 找到该驱动程序违反该规则。

```
G:\Windows-driver-samples\tools\sdv\samples\SDV-FailDriver-WDM\driver>msbuild /p:Configuration=Release /p:Platform=x64 /t:sdv /p:inputs=/check:spinlock
Microsoft (R) Build Engine version 15.6.82.30579 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 3/30/2018 10:56:50 AM.
Project "G:\Windows-driver-samples\tools\sdv\samples\SDV-FailDriver-WDM\driver\fail_driver1.vcxproj" on node 1 (sdv tar
get(s)).
sdv:
  staticdv /check:spinlock
  SDV: H:\Program Files\Windows Kits\10\TOOLS\SDV
  SMV: H:\Program Files\Windows Kits\10\TOOLS\SDV\smv
  SDVAP: H:\Program Files\Windows Kits\10\TOOLS\SDV\smv\analysisplugins\sdv
  Build environment: msbuild
  [INFO] Cleaning ...
  [INFO] Setting interceptor platform to x64
  [INFO] Setting platform to x86_amd64
  [INFO] Validating XML against schema: H:\Program Files\Windows Kits\10\TOOLS\SDV\smv\bin\Config.xsd
  [INFO] Running local scheduler with 8 threads
  [INFO] Driver type found: wdm
  [INFO] Currently reading and validating XML settings from H:\Program Files\Windows Kits\10\TOOLS\SDV\data\wdm\sdv-def
  ault.xml

  [INFO] 1 of 2 jobs remaining. Avg(s): 8.00. Std.Dev(s): 0.00
  [INFO] 1 of 3 jobs remaining. Avg(s): 9.00. Std.Dev(s): 1.00
  Scan ...Done

  [INFO] 0 of 3 jobs remaining. Avg(s): 6.00. Std.Dev(s): 4.32

  Building ...Done
  [INFO] Using plugin SdvPlugin.SmvSdv for analysis.
  [INFO] Running analysis on 11 precondition(s) & 1 rule(s) ...
  [INFO] Checking preconditions...

  [INFO] 10 of 15 jobs remaining. Avg(s): 7.20. Std.Dev(s): 3.66
  [INFO] 10 of 16 jobs remaining. Avg(s): 7.50. Std.Dev(s): 3.40
  [INFO] 11 of 17 jobs remaining. Avg(s): 7.50. Std.Dev(s): 3.40
  [INFO] 10 of 18 jobs remaining. Avg(s): 9.13. Std.Dev(s): 4.08
  [INFO] 11 of 19 jobs remaining. Avg(s): 9.13. Std.Dev(s): 4.08
  [INFO] 10 of 20 jobs remaining. Avg(s): 11.30. Std.Dev(s): 5.68
  [INFO] 11 of 21 jobs remaining. Avg(s): 11.30. Std.Dev(s): 5.68
  [INFO] 11 of 22 jobs remaining. Avg(s): 12.18. Std.Dev(s): 6.09
  [INFO] 10 of 22 jobs remaining. Avg(s): 11.92. Std.Dev(s): 5.89
  [INFO] 10 of 23 jobs remaining. Avg(s): 12.15. Std.Dev(s): 5.72
  [INFO] 10 of 24 jobs remaining. Avg(s): 12.64. Std.Dev(s): 5.79
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 7 of 25 jobs remaining. Avg(s): 13.50. Std.Dev(s): 5.80
  [INFO] 6 of 25 jobs remaining. Avg(s): 13.42. Std.Dev(s): 5.65
  [INFO] 5 of 25 jobs remaining. Avg(s): 13.75. Std.Dev(s): 5.69
  [INFO] 4 of 25 jobs remaining. Avg(s): 13.95. Std.Dev(s): 5.63
  [INFO] 3 of 25 jobs remaining. Avg(s): 14.09. Std.Dev(s): 5.53
  [INFO] 2 of 25 jobs remaining. Avg(s): 14.13. Std.Dev(s): 5.42
  [INFO] 1 of 25 jobs remaining. Avg(s): 14.17. Std.Dev(s): 5.30
  [INFO] 0 of 25 jobs remaining. Avg(s): 14.20. Std.Dev(s): 5.20
  [INFO] Precondition check(s) completed.
  [INFO] Verifying rules...

  [INFO] 1 of 27 jobs remaining. Avg(s): 13.65. Std.Dev(s): 5.78
  [INFO] 1 of 28 jobs remaining. Avg(s): 13.37. Std.Dev(s): 5.86
  [INFO] 0 of 28 jobs remaining. Avg(s): 13.21. Std.Dev(s): 5.81

  [INFO] 1 defects found.
  [INFO] Please review using '/view' argument for SDV.

  [INFO] Total time taken 96 seconds
  [INFO] Found 1 bugs!
Done Building Project "G:\Windows-driver-samples\tools\sdv\samples\SDV-FailDriver-WDM\driver\fail_driver1.vcxproj" (sdv
 target(s)).


Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:01:37.93
```

在查看结果摘要以查看违反了哪些规则之后, 可以指定 **/查看**中可查看静态报表。 驱动程序验证程序的 MSBuild 命令的选项。 有关命令选项的信息，请参阅[Static Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md)。 璝惠**扫描**，**生成**并**检查**步骤在输出中，请参阅[验证过程](verification-process.md)。

下表描述了可以出现在结果摘要中的结果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结果类型</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>规则将传递</strong></p></td>
<td align="left"><p>SDV 通过验证，但无法证明规则的任何冲突的规则数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>缺陷</strong></p></td>
<td align="left"><p>SDV 检测到的规则冲突数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>不适用</strong></p></td>
<td align="left"><p>SDV 无法验证，因为该驱动程序不支持的入口点所需的分析，或该驱动程序未调用的函数的规则监视的规则数。</p>
<p>如果此值大于 0，确认<a href="sdv-map-h.md" data-raw-source="[Sdv-map.h](sdv-map-h.md)">Sdv map.h</a>文件内容正确无误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>超时</strong></p></td>
<td align="left"><p>SDV 停止验证，因为它超出了时间限制为验证每个规则的规则数。 设置时间限制<a href="static-driver-verifier-options-file.md" data-raw-source="[Static Driver Verifier Options File](static-driver-verifier-options-file.md)">静态驱动程序验证工具选项文件</a>，Sdv default.xml。</p>
<p>SDV 中的限制被由于此结果。 它并不表示该驱动程序中的错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Spaceouts</strong></p></td>
<td align="left"><p>SDV 停止验证，因为它超出了验证规则的内存限制的规则数。 在中设置的内存限制<a href="static-driver-verifier-options-file.md" data-raw-source="[Static Driver Verifier Options File](static-driver-verifier-options-file.md)">静态驱动程序验证工具选项文件</a>，Sdv default.xml。</p>
<p>SDV 中的限制被由于此结果。 它并不表示该驱动程序中的错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>其他</strong></p></td>
<td align="left"><p>SDV 遇到内部错误从中它无法恢复的次数。</p></td>
</tr>
</tbody>
</table>

 

 

 





