---
title: wrmsr（写入 MSR）
description: Wrmsr 命令将一个值写入 Model-Specific 将 (MSR) 注册到指定地址。
keywords:
- wrmsr (编写 MSR) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wrmsr (Write MSR)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5bb2ddf1060af217cb2c6f2f8fc206c77a5cd58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802735"
---
# <a name="wrmsr-write-msr"></a>wrmsr（写入 MSR）


**Wrmsr** 命令将一个值写入 Model-Specific 将 (MSR) 注册到指定地址。

`wrmsr Address Value`

## <a name="span-idddk_cmd_write_msr_dbgspanspan-idddk_cmd_write_msr_dbgspanparameters"></a><span id="ddk_cmd_write_msr_dbg"></span><span id="DDK_CMD_WRITE_MSR_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 MSR 的地址。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*值*   
指定要写入到 MSR 的64位十六进制值。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Wrmsr** 命令可在基于 x86 和基于 x64 的平台上显示 MSR。 MSR 定义是特定于平台的。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**rdmsr（读取 MSR）**](rdmsr--read-msr-.md)

 

 






