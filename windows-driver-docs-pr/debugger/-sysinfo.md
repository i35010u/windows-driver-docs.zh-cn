---
title: sysinfo
description: Sysinfo 扩展读取并显示指定的 SMBIOS、高级配置和电源接口 (ACPI) 以及转储文件或实时系统中的 CPU 信息。
keywords:
- sysinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sysinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58484bb004ddefd9e88c4333da27f237adf945e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830319"
---
# <a name="sysinfo"></a>!sysinfo


**！ Sysinfo** extension 读取并显示指定的 SMBIOS、高级配置和电源接口 (ACPI) 以及转储文件或实时系统中的 CPU 信息。

```dbgcmd
!sysinfo cpuinfo [-csv [-noheaders]]
!sysinfo cpumicrocode [-csv [-noheaders]]
!sysinfo cpuspeed [-csv [-noheaders]]
!sysinfo gbl [-csv [-noheaders]]
!sysinfo machineid [-csv [-noheaders]]
!sysinfo registers
!sysinfo smbios [-csv [-noheaders]] {-debug | -devices | -memory | -power | -processor | -system | -v} 
!sysinfo -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______cpuinfo______"></span><span id="_______CPUINFO______"></span>**cpuinfo**   
显示有关处理器的信息。

<span id="_______cpumicrocode______"></span><span id="_______CPUMICROCODE______"></span>**cpumicrocode**   
 (GenuineIntel 处理器仅) 显示初始和缓存的微码处理器版本。

<span id="_______cpuspeed______"></span><span id="_______CPUSPEED______"></span>**cpuspeed**   
显示最大和当前处理器速度。

<span id="_______gbl______"></span><span id="_______GBL______"></span>**gbl**   
显示 ACPI 表的 BIOS 列表。

<span id="_______machineid______"></span><span id="_______MACHINEID______"></span>**machineid**   
显示 SMBIOS、BIOS、固件、系统和基板的计算机 ID 信息。

<span id="_______registers______"></span><span id="_______REGISTERS______"></span>**注册**   
显示 (MSRs) 的计算机特定寄存器。

<span id="_______smbios______"></span><span id="_______SMBIOS______"></span>**smbios**   
显示 SMBIOS 表。

<span id="_______-csv______"></span><span id="_______-CSV______"></span>**-csv**   
以逗号分隔的可变长度 (CSV) 格式显示所有数据。

<span id="_______-noheaders______"></span><span id="_______-NOHEADERS______"></span>**-noheaders**   
禁止 CSV 格式的标头。

<span id="_______-debug______"></span><span id="_______-DEBUG______"></span>**-调试**   
显示标准格式和 CSV 格式的输出。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span>**-设备**   
显示 SMBIOS 表中的设备条目。

<span id="_______-memory______"></span><span id="_______-MEMORY______"></span>**-内存**   
显示 SMBIOS 表中的内存项。

<span id="_______-power______"></span><span id="_______-POWER______"></span>**-power**   
显示 SMBIOS 表中的电源项。

<span id="_______-processor______"></span><span id="_______-PROCESSOR______"></span>**-处理器**   
显示 SMBIOS 表中的处理器条目。

<span id="_______-system______"></span><span id="_______-SYSTEM______"></span>**-系统**   
显示 SMBIOS 表中的系统项。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
“详细”： 显示 SMBIOS 表中条目的详细信息。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的帮助命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 基本系统</strong></p>
<p><strong>Windows 2003 基本系统</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows XP Service Pack 2 及更高版本</strong></p>
<p><strong>Windows 2003，Service Pack 1 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

仅当转储文件是系统崩溃文件 ( dmp) ，该文件尚未从内核或完整转储文件转换为小型转储文件，或者实时系统已开始启动并且处于联机 (状态时（例如，在登录提示) 时），此扩展插件非常有用。

可以在单个扩展命令中使用 **-debug**、 **-devices**、 **-memory**、 **-power**、 **-processor**、- **system** 和 **-v** 参数的任意组合。

仅在特定系统上支持以下参数：

- 仅当目标计算机支持 ACPI 时， **gbl** 参数才有效。

- 仅当目标计算机支持 SMBIOS 时， **smbios** 参数才有效。

Microsoft 将从这些记录中 (PII) 删除个人身份信息。 将从转储文件中删除所有 PII。 但是，在实时系统上，某些 PII 可能尚未删除。 因此，PII 字段将报告为0或空，即使它们确实包含信息。

若要在任何时候停止执行包含 **cpuinfo**、 **gbl**、 **寄存器** 或 **Smbios** 参数的命令，请在 WinDbg) 中按 ctrl + BREAK (或在 KD) 中按 ctrl + C (。
