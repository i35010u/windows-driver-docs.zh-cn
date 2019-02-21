---
title: rdmsr (读取 MSR)
description: Rdmsr 命令读取模型特定注册 (MSR) 值从指定的地址。
ms.assetid: 693f1be5-f215-4719-ae6f-30e367cefd77
keywords:
- rdmsr (读取 MSR) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rdmsr (Read MSR)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be90d702d97c5eedd5b47254d33d873610264ca4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540394"
---
# <a name="rdmsr-read-msr"></a>rdmsr (读取 MSR)


**Rdmsr**命令读取[模型特定注册 (MSR)](other-data-spaces.md)值从指定的地址。

```dbgcmd
rdmsr Address 
```

## <a name="span-idddkcmdreadmsrdbgspanspan-idddkcmdreadmsrdbgspanparameters"></a><span id="ddk_cmd_read_msr_dbg"></span><span id="DDK_CMD_READ_MSR_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 MSR 的地址。

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

 

<a name="remarks"></a>备注
-------

**Rdmsr**命令可在基于 x86 的、 基于 Itanium 和基于 x64 的平台上显示 MSR 的。 MSR 定义是特定于平台的。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**wrmsr (Write MSR)**](wrmsr--write-msr-.md)

 

 






