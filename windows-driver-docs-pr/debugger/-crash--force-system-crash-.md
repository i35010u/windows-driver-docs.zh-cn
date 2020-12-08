---
title: .crash（强制系统崩溃）
description: 崩溃命令会导致目标计算机发出 bug 检查。
keywords:
- 。崩溃 (强制系统崩溃) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .crash (Force System Crash)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f461bc599d3dbee9fee4443d7b221a220d98db12
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803331"
---
# <a name="crash-force-system-crash"></a>.crash（强制系统崩溃）


**崩溃** 命令会导致目标计算机发出 bug 检查。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关相关命令的概述以及系统崩溃后可用选项的说明，请参阅 [崩溃并重新启动目标计算机](crashing-and-rebooting-the-target-computer.md)。

<a name="remarks"></a>备注
-------

此命令会立即导致目标计算机出现故障。

如果你已经处于 bug 检查处理程序中，请不要使用 **。** 改用 [**g (转)**](g--go-.md) 来继续执行处理程序，这将生成故障转储。

如果启用了故障转储，将写入内核模式转储文件。 有关详细信息，请参阅 [创建 Kernel-Mode 转储文件](creating-a-kernel-mode-dump-file.md) 。

 

 





