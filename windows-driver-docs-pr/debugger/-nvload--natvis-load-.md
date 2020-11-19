---
title: .nvload（NatVis 加载）
description: Nvload 命令将 NatVis 文件加载到调试器环境中。 在可视化效果加载后，它将用于呈现可视化对象中定义的数据。
ms.assetid: 9B14B3B4-EA90-426E-8555-0E5B8F63E0A9
keywords:
- nvload (NatVis) Windows 调试的负载
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .nvload (NatVis Load)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6dc22de05ac2dae4e974ef3b55602bb24c021417
ms.sourcegitcommit: 878a1cb0149dc18ccbd31774e12bad76084dfa24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2020
ms.locfileid: "94937771"
---
# <a name="nvload-natvis-load"></a>.nvload（NatVis 加载）


Nvload 命令将 NatVis 文件加载到调试器环境中。 在可视化效果加载后，它将用于呈现可视化对象中定义的数据。

```dbgcmd
.nvload FileName|ModuleName
```

## <a name="parameters"></a>参数

*FileName |ModuleName*

指定要加载的 NatVis 文件名或模块名称。

**FileName** 是要加载的 natvis 文件的显式名称。 可以使用完全限定的路径。

**ModuleName** 是正在调试的目标进程中的模块的名称。 如果有任何可用的，则将加载嵌入到符号文件 (PDB) 命名模块名称的所有 NatVis 文件。

## <a name="environment"></a>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

## <a name="additional-information"></a>其他信息

有关详细信息，请参阅 [创建本机对象的自定义视图](/visualstudio/debugger/create-custom-views-of-native-objects)。

## <a name="see-also"></a>请参阅

[**dx (显示 NatVis 表达式)**](dx--display-visualizer-variables-.md)