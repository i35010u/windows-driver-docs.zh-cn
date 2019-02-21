---
title: vad_reload
description: Vad_reload 扩展重新指定进程的用户模式模块加载使用该过程的虚拟地址说明符 (Vad)。
ms.assetid: B5500227-DDC5-43aa-987B-EB02C59B3AC6
keywords:
- vad_reload Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vad_reload
api_location:
- Kdextx86.dll
- Kdexts.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.openlocfilehash: be367b22f5f80dbfcb90299884972d350deeb009
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525373"
---
# <a name="vadreload"></a>！ vad\_重新加载


**！ Vad\_重新加载**扩展使用该过程的虚拟地址说明符 (Vad)，则重新加载指定的进程的用户模式模块。

```dbgcmd
!vad_reload Process
```

## <a name="span-idddkvaddbgspanspan-idddkvaddbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
指定将为其加载模块的过程的十六进制地址。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

Vad 有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这本书不可能在某些语言和国家/地区中可用。）

<a name="remarks"></a>备注
-------

可以使用[ **！ 过程**](-process.md)扩展，若要查找进程的地址。

下面是举例说明如何查找地址，并将其 **！ vad\_重新加载**命令。

```dbgcmd
3: kd> !process 0 0
. . .
PROCESS fffffa8007d54450
    SessionId: 1  Cid: 115c    Peb: 7ffffef6000  ParentCid: 0c58
    DirBase: 111bc3000  ObjectTable: fffff8a006ae0960  HandleCount: 229.
    Image: SearchProtocolHost.exe
. . .
3: kd> !vad_reload fffffa8007d54450
fffffa80`04f5e8b0: VAD maps 00000000`6c230000 - 00000000`6c26bfff, file cscobj.dll
fffffa80`04e8f890: VAD maps 00000000`6ef90000 - 00000000`6f04afff, file mssvp.dll
fffffa80`07cbb010: VAD maps 00000000`6f910000 - 00000000`6faf5fff, file tquery.dll
fffffa80`08c1f2a0: VAD maps 00000000`6fb80000 - 00000000`6fb9bfff, file mssprxy.dll
fffffa80`07dce8b0: VAD maps 00000000`6fba0000 - 00000000`6fba7fff, file msshooks.dll
fffffa80`04fd2e70: VAD maps 00000000`72a50000 - 00000000`72a6cfff, file userenv.dll
. . .
```

<a name="requirements"></a>要求
------------

**DLL**

Kdexts.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!process**](-process.md)

[**!vad**](-vad.md)

 

 






