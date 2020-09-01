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
ms.openlocfilehash: 92ecfe2e0778882a147514902c0c507b20de32e5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211254"
---
# <a name="nvload-natvis-load"></a>.nvload（NatVis 加载）


Nvload 命令将 NatVis 文件加载到调试器环境中。 在可视化效果加载后，它将用于呈现可视化对象中定义的数据。

```dbgcmd
.nvload FileName|ModuleName
```

## <a name="parameters"></a>参数

*FileName |ModuleName*

指定要加载的 NatVis 文件名或模块名称。

**FileName**是要加载的 natvis 文件的显式名称。 可以使用完全限定的路径。

**ModuleName**是正在调试的目标进程中的模块的名称。 如果有任何可用的，则将加载嵌入到符号文件 (PDB) 命名模块名称的所有 NatVis 文件。

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

有关详细信息，请参阅 [创建本机对象的自定义视图](/visualstudio/debugger/create-custom-views-of-native-objects?view=vs-2015)。

## <a name="see-also"></a>另请参阅

[**dx (显示 NatVis 表达式) **](dx--display-visualizer-variables-.md)