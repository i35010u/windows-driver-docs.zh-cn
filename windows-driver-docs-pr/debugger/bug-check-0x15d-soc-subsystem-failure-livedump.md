---
title: Bug 检查 0x15D SOC_SUBSYSTEM_FAILURE_LIVEDUMP
description: SOC_SUBSYSTEM_FAILURE_LIVEDUMP bug 代码具有 0x0000015D 值。
ms.assetid: F7903E88-1706-46E6-A5D0-6972702058A8
keywords:
- Bug 检查 0x15D SOC_SUBSYSTEM_FAILURE_LIVEDUMP
- Bug 检查 0x14B SOC_SUBSYSTEM_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Bug Check 0x14B SOC_SUBSYSTEM_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1af822a5b3cd92ebfb9b5bdb8ccb4000ebbec66c
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239814"
---
# <a name="bug-check-0x15d-socsubsystemfailurelivedump"></a>Bug 检查 0x15D：SOC\_SUBSYSTEM\_FAILURE\_LIVEDUMP


SOC\_子系统\_失败\_LIVEDUMP 错误代码的值为 0x0000015D。 这表示芯片 (SoC) 子系统上的系统遇到严重故障，并且已捕获的实时内核转储。 SoC 子系统不在此情况下生成的 bug 检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="bug-check-0x14b-socsubsystemfailure-parameters"></a>Bug 检查 0x14B SOC\_子系统\_失败参数


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
<td align="left"><p>地址<strong><a href="https://msdn.microsoft.com/library/windows/hardware/dn376404" data-raw-source="[SOC_SUBSYSTEM_FAILURE_DETAILS](https://msdn.microsoft.com/library/windows/hardware/dn376404)">SOC_SUBSYSTEM_FAILURE_DETAILS</a></strong>结构。</p></td>
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

 

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

使用提供的 nt ！SOC\_子系统\_失败\_要转储使用 dt 命令，并提供 Arg1 的地址的故障数据的详细信息结构。

```dbgcmd
2: kd> dt nt!SOC_SUBSYSTEM_FAILURE_DETAILS 9aa8d630
   +0x000 SubsysType       : 1 ( SOC_SUBSYS_AUDIO_DSP )
   +0x008 FirmwareVersion  : 0
   +0x010 HardwareVersion  : 0
   +0x018 UnifiedFailureRegionSize : 0x24
   +0x01c UnifiedFailureRegion : [1]  "F"
```

适用于 SoC 供应商，以进一步分析数据，包括可选的供应商提供常规用途数据块。

你可能想要检查堆栈跟踪使用[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。 您可以指定要检查堆栈上的所有处理器的处理器数。

此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

-   检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   您可以尝试运行硬件诊断程序提供的系统制造商。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

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

 

 




