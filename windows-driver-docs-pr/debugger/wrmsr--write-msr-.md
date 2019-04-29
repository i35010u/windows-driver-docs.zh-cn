---
title: wrmsr（写入 MSR）
description: Wrmsr 命令写入到特定于模型的注册 (MSR) 指定地址处的值。
ms.assetid: fe90b984-e2d6-4af7-b708-56fbcd2bbadd
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
ms.openlocfilehash: 8b8391757e58bd6941cd717b6c446229cd6d147e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381924"
---
# <a name="wrmsr-write-msr"></a>wrmsr（写入 MSR）


**Wrmsr**命令将值写入到特定于模型的注册 (MSR) 在指定的地址。

`wrmsr Address Value`

## <a name="span-idddkcmdwritemsrdbgspanspan-idddkcmdwritemsrdbgspanparameters"></a><span id="ddk_cmd_write_msr_dbg"></span><span id="DDK_CMD_WRITE_MSR_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 MSR 的地址。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *值*   
指定要写入到 MSR 的 64 位十六进制值。

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

**Wrmsr**命令可在基于 x86 的、 基于 Itanium 和基于 x64 的平台上显示 MSR 的。 MSR 定义是特定于平台的。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**rdmsr (Read MSR)**](rdmsr--read-msr-.md)

 

 






