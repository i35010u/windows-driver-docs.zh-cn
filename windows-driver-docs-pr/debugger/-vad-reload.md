---
title: vad_reload
description: Vad_reload 扩展使用该进程 (Vad) 的虚拟地址描述符为指定的进程重载用户模式模块。
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
ms.openlocfilehash: 8b88baf7ce22ae643238e37124469dc945acb6d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833847"
---
# <a name="vad_reload"></a>！ vad \_ 重载


**！ Vad \_ reload** extension 使用该进程的虚拟地址描述符 (vad) 为指定的进程重新加载用户模式模块。

```dbgcmd
!vad_reload Process
```

## <a name="span-idddk__vad_dbgspanspan-idddk__vad_dbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
指定将为其加载模块的进程的十六进制地址。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 Vad 的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。 

<a name="remarks"></a>备注
-------

您可以使用 [**！进程**](-process.md) 扩展查找进程的地址。

下面是一个示例，演示如何查找地址并将其用于 **！ vad \_ reload.sql** 命令。

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

**.DLL**

Kdexts.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**！进程**](-process.md)

[**!vad**](-vad.md)

 

 






