---
title: 命令行输出
description: 命令行输出
keywords:
- 输出文件 WDK 静态驱动程序验证程序
- 命令行输出 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96b41aae12d4c32e41a996b0da889688e081625a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837811"
---
# <a name="command-line-output"></a>命令行输出


将命令提交到 SDV 时，它会在执行命令时显示有关该命令的信息、指示该命令是成功还是失败的状态消息，以及可能已生成的任何错误消息或警告。 验证结果的摘要显示在输出的底部。

例如，下图显示了命令中的命令行输出，用于验证包含 [旋转锁](wdm-spinlock.md) 规则的 SDV-FAILDRIVER-WDM 示例驱动程序。 SDV-FailDriver-WDM 示例驱动程序（包含有意编码错误的驱动程序）位于 \\ \\ \\ \\ Windows 驱动程序示例的 tools SDV samples SDV-FailDriver-WDM 文件夹中。

在此验证中，SDV 发现驱动程序违反了该规则。

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

查看结果摘要以查看违反了哪些规则后，可以在 MSBuild 命令中指定 **/view** 选项，以查看静态驱动程序验证程序报表。 有关命令选项的信息，请参阅 [静态驱动程序验证程序命令 (MSBuild) ](-static-driver-verifier-commands--msbuild-.md)。 有关 **扫描**、 **构建** 和 **检查** 输出中的步骤的信息，请参阅 [验证过程](verification-process.md)。

下表描述了可能出现在结果摘要中的结果。

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
<td align="left"><p><strong>规则通过</strong></p></td>
<td align="left"><p>SDV 验证的规则数，但无法证明规则的任何冲突。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>缺陷</strong></p></td>
<td align="left"><p>SDV 检测到的规则冲突的数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>不适用</strong></p></td>
<td align="left"><p>由于驱动程序不支持分析所需的入口点或驱动程序未调用规则所监视的函数，SDV 无法验证的规则数。</p>
<p>如果此值大于0，请验证 <a href="sdv-map-h.md" data-raw-source="[Sdv-map.h](sdv-map-h.md)">Sdv</a> 文件的内容是否正确。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>超时值</strong></p></td>
<td align="left"><p>SDV 停止验证的规则数，因为它超过了验证每个规则的时间限制。 时间限制设置为 <a href="static-driver-verifier-options-file.md" data-raw-source="[Static Driver Verifier Options File](static-driver-verifier-options-file.md)">静态驱动程序验证程序选项文件</a>，Sdv-default.xml。</p>
<p>此结果由 SDV 中的限制引起。 它不指示驱动程序中的错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Spaceouts</strong></p></td>
<td align="left"><p>SDV 停止验证的规则数，因为它超过了用于验证该规则的内存限制。 内存限制在 <a href="static-driver-verifier-options-file.md" data-raw-source="[Static Driver Verifier Options File](static-driver-verifier-options-file.md)">静态驱动程序验证程序选项文件</a>中设置 Sdv-default.xml。</p>
<p>此结果由 SDV 中的限制引起。 它不指示驱动程序中的错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>其他</strong></p></td>
<td align="left"><p>SDV 遇到无法从中恢复的内部错误的次数。</p></td>
</tr>
</tbody>
</table>

 

 

 





