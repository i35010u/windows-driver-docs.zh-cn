---
title: Bug 检查 0x14B SOC_SUBSYSTEM_FAILURE
description: SOC_SUBSYSTEM_FAILURE bug 检查的值为0x0000014B。 这表明芯片 (SoC) 子系统上的系统中发生了不可恢复的错误。
keywords:
- Bug 检查 0x14B SOC_SUBSYSTEM_FAILURE
- Bug 检查 0x14B SOC_SUBSYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Bug Check 0x14B SOC_SUBSYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e231a4e60b9aca92b14d437e5aa244f97ec291b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790723"
---
# <a name="bug-check-0x14b-soc_subsystem_failure"></a>Bug 检查0x14B： SOC \_ 子系统 \_ 故障


SOC \_ 子系统 \_ 失败 bug 检查的值为0x0000014B。 这表明芯片 (SoC) 子系统上的系统中发生了不可恢复的错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="bug-check-0x14b-soc_subsystem_failure-parameters"></a>Bug 检查 0x14B SOC \_ 子系统 \_ 故障参数


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
<td align="left"><p><strong><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_soc_subsystem_failure_details" data-raw-source="[SOC_SUBSYSTEM_FAILURE_DETAILS](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_soc_subsystem_failure_details)">SOC_SUBSYSTEM_FAILURE_DETAILS</a></strong>结构的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>可选。 供应商提供的数据块的地址。</p></td>
</tr>
</tbody>
</table>

 

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

```dbgcmd
2: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

SOC_SUBSYSTEM_FAILURE (14b)
A SOC subsystem has experienced an unrecoverable critical fault.
Arguments:
Arg1: 9aa8d630, nt!SOC_SUBSYSTEM_FAILURE_DETAILS
Arg2: 00000000, Reserved
Arg3: 00000000, Reserved
Arg4: a126c000, (Optional) address to vendor supplied general purpose data block.
```

使用提供的 nt！SOC \_ 子系统 \_ 故障 \_ 详细信息结构，使用 Dt 命令和 Arg1 提供的地址转储故障数据。

```dbgcmd
2: kd> dt nt!SOC_SUBSYSTEM_FAILURE_DETAILS 9aa8d630
   +0x000 SubsysType       : 1 ( SOC_SUBSYS_AUDIO_DSP )
   +0x008 FirmwareVersion  : 0
   +0x010 HardwareVersion  : 0
   +0x018 UnifiedFailureRegionSize : 0x24
   +0x01c UnifiedFailureRegion : [1]  "F"
```

使用 SoC 供应商进一步分析数据，包括可选供应商提供的常规用途数据块。

你可能想要使用 [**k、kb、glm-kc-qnw、kd、kp、kp、kv (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来检查堆栈跟踪。 可以指定处理器编号来检查所有处理器上的堆栈。

你还可以在代码中设置一个断点，使其导致此 stop 代码，并尝试单步执行出错的代码。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

如果你不具备使用 Windows 调试器来处理此问题，则可以使用一些基本的故障排除技术。

-   查看事件查看器中的系统日志，以获取可能有助于识别导致此错误检查的设备或驱动程序的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   你可以尝试运行系统制造商提供的硬件诊断。

-   有关其他常规疑难解答信息，请参阅 [**蓝屏数据**](blue-screen-data.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
</tbody>
</table>

