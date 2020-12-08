---
title: storagekd.storsrb
description: Storagekd. storsrb 扩展显示有关指定存储 (或 SCSI) 请求块 (SRB) 的信息。
keywords:
- storagekd storsrb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storsrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d6024b7c2c4cda7e95c8c09897e3fbe0d410e728
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817009"
---
# <a name="storagekdstorsrb"></a>!storagekd.storsrb


**！ Storagekd; storsrb** 扩展显示有关指定的存储 (或 SCSI) 请求块 (SRB) 的信息。

```dbgcmd
!storagekd.storsrb Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span>*地址*  
指定 SRB 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是 **！ storsrb** 显示的示例 storagekd：

**0： kd &gt; ！ storagekd. storsrb ffffe00111fe25b0**

```dbgcmd
    SRB is a STORAGE request block (SRB_EX)
    SRB EX 0xffffe00111fe25b0 Function 28  Version  1, Signature 53524258, SrbStatus: 0x02[Aborted], SrbFunction 0x00 [EXECUTE SCSI]
    Address Type is BTL8

       SRB_EX Data Type [SrbExDataTypeScsiCdb16] 
    [EXECUTE SCSI] SRB_EX: 0xffffe00111fe2648  OriginalRequest: 0xffffe001125a9010  DataBuffer/Length: 0xffffe00112944000 / 0x00000200
    PTL: (0, 1, 1)  CDB: 28 00 00 00 00 00 00 00 01 00 00 00 00 00 00 00  OpCode: SCSI/READ (10)   
```

 

 





