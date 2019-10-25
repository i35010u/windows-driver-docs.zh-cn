---
title: .errlog
description: .Errlog 扩展在 i/o 系统的错误日志中显示任何挂起项的内容。
ms.assetid: 2ef6331e-fa83-4515-8d70-5094e40b8497
keywords:
- .errlog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errlog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 15ee478076f0db2fa073f31464ace6e1c5cbd9f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826761"
---
# <a name="errlog"></a>!errlog


**！ .Errlog** extension 显示 i/o 系统的错误日志中任何挂起项的内容。

```dbgcmd
!errlog 
```

## <span id="ddk__errlog_dbg"></span><span id="DDK__ERRLOG_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关[**IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)的信息，请参阅 Windows 驱动程序工具包（WDK）文档。

<a name="remarks"></a>备注
-------

此命令显示有关 i/o 系统的错误日志中任何挂起事件的信息。 这些事件由对[**IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)函数的调用排队等候写入系统的事件日志，以便**事件查看器**以后查看。

仅显示由[**IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)排队但未提交到错误日志的条目。

此命令可在系统崩溃后用作诊断帮助，因为它会显示在系统停止之前无法提交到错误日志的挂起错误信息。

 

 





