---
title: storagekd.storsrb
description: Storagekd.storsrb 扩展显示有关指定的存储 （或 SCSI） 的信息请求块 (SRB)。
ms.assetid: E2AB3BE2-0EE1-4FB5-9F62-02169B22B00B
keywords:
- storagekd.storsrb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storsrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 67a04170a375b54f772a584566f6ad815cea4fd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338786"
---
# <a name="storagekdstorsrb"></a>!storagekd.storsrb


**！ Storagekd.storsrb**扩展显示有关指定的存储 （或 SCSI） 的信息请求块 (SRB)。

```dbgcmd
!storagekd.storsrb Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span> *Address*  
指定 SRB 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是举例 **！ storagekd.storsrb**显示：

**0: kd&gt; !storagekd.storsrb ffffe00111fe25b0**

```dbgcmd
    SRB is a STORAGE request block (SRB_EX)
    SRB EX 0xffffe00111fe25b0 Function 28  Version  1, Signature 53524258, SrbStatus: 0x02[Aborted], SrbFunction 0x00 [EXECUTE SCSI]
    Address Type is BTL8

       SRB_EX Data Type [SrbExDataTypeScsiCdb16] 
    [EXECUTE SCSI] SRB_EX: 0xffffe00111fe2648  OriginalRequest: 0xffffe001125a9010  DataBuffer/Length: 0xffffe00112944000 / 0x00000200
    PTL: (0, 1, 1)  CDB: 28 00 00 00 00 00 00 00 01 00 00 00 00 00 00 00  OpCode: SCSI/READ (10)   
```

 

 





