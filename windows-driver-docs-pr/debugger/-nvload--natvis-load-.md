---
title: .nvload（NatVis 加载）
description: Nvload 命令将 NatVis 文件加载到调试器环境中。 在可视化效果加载后，它将用于呈现可视化对象中定义的数据。
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
ms.openlocfilehash: 98f4cbcd33add62877f3e448a0206a1a10424178
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803297"
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
