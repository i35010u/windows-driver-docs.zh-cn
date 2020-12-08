---
title: .srcnoisy（干扰性源加载）
description: Srcnoisy 命令控制源文件加载的详细级别。
keywords:
- srcnoisy (噪音源加载) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcnoisy (Noisy Source Loading)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab5ee52a281f8f0d6291eb0f19f836a978a92f19
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811243"
---
# <a name="srcnoisy-noisy-source-loading"></a>.srcnoisy（干扰性源加载）


**Srcnoisy** 命令控制源文件加载的详细级别。

```dbgcmd
.srcnoisy [Options]
```

## <a name="span-idddk_meta_noisy_source_loading_dbgspanspan-idddk_meta_noisy_source_loading_dbgspanparameters"></a><span id="ddk_meta_noisy_source_loading_dbg"></span><span id="DDK_META_NOISY_SOURCE_LOADING_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可以是下列选项之一：

<span id="0"></span>0  
禁用显示额外消息。

<span id="1"></span>1  
显示有关源文件的加载和卸载进度的信息。

<span id="2"></span>2  
显示有关符号文件的加载和卸载进度的信息。

<span id="3"></span>三维空间  
显示选项1和2显示的所有信息。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

不带参数的 **srcnoisy** 将显示当前加载噪音源的状态。

不应将干扰性源加载与干扰符号加载相混淆，这是由 [**！符号干扰**](-sym.md) 扩展和控制 [SYMOPT \_ 调试](symbol-options.md#symopt-debug) 设置的其他方式控制的。

 

 





