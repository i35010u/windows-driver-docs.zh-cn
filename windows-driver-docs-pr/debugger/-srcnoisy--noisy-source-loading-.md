---
title: .srcnoisy（干扰性源加载）
description: 可通过.srcnoisy 命令控制源文件加载的详细级别。
ms.assetid: c57e0d0a-7903-455a-9a92-fab75f10ca80
keywords:
- 可通过.srcnoisy （干扰源加载） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcnoisy (Noisy Source Loading)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aac70c4217d3cfef3f58b2b52aeabe4435d8f385
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334248"
---
# <a name="srcnoisy-noisy-source-loading"></a>.srcnoisy（干扰性源加载）


**可通过.srcnoisy**命令控制源文件加载的详细级别。

```dbgcmd
.srcnoisy [Options]
```

## <a name="span-idddkmetanoisysourceloadingdbgspanspan-idddkmetanoisysourceloadingdbgspanparameters"></a><span id="ddk_meta_noisy_source_loading_dbg"></span><span id="DDK_META_NOISY_SOURCE_LOADING_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以是下列选项之一：

<span id="0"></span>0  
禁止显示多出的信息。

<span id="1"></span>1  
显示源文件加载和卸载的进度有关的信息。

<span id="2"></span>2  
显示的符号文件加载和卸载进度有关的信息。

<span id="3"></span>3  
显示通过选项 1 和 2 显示的所有信息。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

不带任何参数，**可通过.srcnoisy**将显示干扰源加载的当前状态。

不将干扰源加载与干扰性的符号加载-由控制相混淆[ **！ 符号干扰**](-sym.md)扩展和通过其他方式的控制[SYMOPT\_调试](symbol-options.md#symopt-debug)设置。

 

 





