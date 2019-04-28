---
title: sysinfo
description: Sysinfo 扩展读取并显示从转储文件或实时系统指定的 SMBIOS、 高级配置和电源接口 (ACPI) 和 CPU 信息。
ms.assetid: 1637fcc8-54ff-46a4-94f4-0b2df38507d1
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
ms.openlocfilehash: 0f9c65d2232e157eb39afdfa1f01d86f4aa2012a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338768"
---
# <a name="sysinfo"></a>!sysinfo


**！ Sysinfo**扩展读取并显示从转储文件或实时系统指定的 SMBIOS、 高级配置和电源接口 (ACPI) 和 CPU 信息。

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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______cpuinfo______"></span><span id="_______CPUINFO______"></span> **cpuinfo**   
显示有关该处理器的信息。

<span id="_______cpumicrocode______"></span><span id="_______CPUMICROCODE______"></span> **cpumicrocode**   
（仅 GenuineIntel 处理器）显示微代码，初始和缓存处理器版本。

<span id="_______cpuspeed______"></span><span id="_______CPUSPEED______"></span> **cpuspeed**   
显示最大值和当前的处理器速度。

<span id="_______gbl______"></span><span id="_______GBL______"></span> **gbl**   
显示 BIOS ACPI 表的列表。

<span id="_______machineid______"></span><span id="_______MACHINEID______"></span> **machineid**   
显示计算机的 SMBIOS、 BIOS、 固件、 系统和基板 ID 信息。

<span id="_______registers______"></span><span id="_______REGISTERS______"></span> **registers**   
显示特定于计算机注册 (MSRs)。

<span id="_______smbios______"></span><span id="_______SMBIOS______"></span> **smbios**   
显示 SMBIOS 表。

<span id="_______-csv______"></span><span id="_______-CSV______"></span> **-csv**   
以逗号分隔、 可变长度 (CSV) 格式显示所有数据。

<span id="_______-noheaders______"></span><span id="_______-NOHEADERS______"></span> **-noheaders**   
禁止显示 CSV 格式的标头。

<span id="_______-debug______"></span><span id="_______-DEBUG______"></span> **-debug**   
标准格式和 CSV 格式显示输出。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span> **-devices**   
SMBIOS 表中显示的设备条目。

<span id="_______-memory______"></span><span id="_______-MEMORY______"></span> **-memory**   
SMBIOS 表中显示内存项。

<span id="_______-power______"></span><span id="_______-POWER______"></span> **-power**   
SMBIOS 表中显示的 power 条目。

<span id="_______-processor______"></span><span id="_______-PROCESSOR______"></span> **-processor**   
SMBIOS 表中显示的处理器条目。

<span id="_______-system______"></span><span id="_______-SYSTEM______"></span> **-system**   
SMBIOS 表中显示系统项。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
详细。 SMBIOS 表中显示项的详细的信息。

<span id="_______-_______"></span> **-?**   
显示此扩展在调试器命令窗口中的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p><strong>Windows XP 基础系统</strong></p>
<p><strong>Windows 2003 的基础系统</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows XP Service Pack 2 及更高版本</strong></p>
<p><strong>Windows 2003 Service Pack 1 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此扩展时，可以仅转储文件是系统崩溃文件 (.dmp) 的项目尚未转换到小型转储文件从内核或完整转储文件，或在活动的系统已经完成启动并处于联机状态 （例如，在登录提示符下）。

可以使用的任意组合 **-调试**， **-设备**， **-内存**， **-power**， **-处理器**，**-系统**，并 **-v**单个扩展命令中的参数。

仅在特定系统上支持以下参数：

-   **Gbl**参数有效仅当目标计算机支持 ACPI。

-   **Smbios**仅当目标计算机支持 SMBIOS 参数有效。

-   **注册**参数不适用于基于 Itanium 的目标计算机上，因为它们不会收集 MSRs。

Microsoft 会竭尽全力从这些记录中删除个人身份信息 (PII)。 从转储文件中删除所有 PII。 但是，在实时系统中，一些 PII 可能尚未删除。 因此，PII 字段将被报告为 0 或留空，即使它们实际上包含的信息。

若要停止执行包含的命令**cpuinfo**， **gbl**，**注册**，或者**smbios**参数在任何时间，按 CTRL + BREAK（在 WinDbg) 或 CTRL + C （中 KD)。

 

 





