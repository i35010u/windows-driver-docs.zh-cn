---
title: .crash（强制系统崩溃）
description: .Crash 命令会使目标计算机发出的 bug 检查。
ms.assetid: 625d174d-7011-4b15-aad7-1b39aa3742a4
keywords:
- .crash （强制系统崩溃） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .crash (Force System Crash)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ef8a05ce1fc60eb642588604c148763d4d77f85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566112"
---
# <a name="crash-force-system-crash"></a>.crash（强制系统崩溃）


**.Crash**命令将导致目标计算机发出的 bug 检查。

```dbgsyntax
.crash
```

## <span id="ddk_meta_force_system_crash_dbg"></span><span id="DDK_META_FORCE_SYSTEM_CRASH_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

相关命令的概述和系统崩溃后可用的选项的说明，请参阅[崩溃和重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

<a name="remarks"></a>备注
-------

此命令将立即导致崩溃的目标计算机。

如果已在 bug 检查处理程序中，不要使用 **.crash**。 使用[ **g （转向）** ](g--go-.md)而是继续执行处理程序，它将生成故障转储。

如果已启用故障转储将写入一个内核模式转储文件。 请参阅[创建内核模式转储文件](creating-a-kernel-mode-dump-file.md)有关详细信息。

 

 





