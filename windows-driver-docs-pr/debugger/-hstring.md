---
title: hstring
description: Hstring 扩展显示 HSTRING 的字段。 显示的最后一项是字符串本身。
keywords:
- hstring Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hstring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 68dcd36b3470d2391510cfd60c6c809eab46ba80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825813"
---
# <a name="hstring"></a>!hstring


**！ Hstring** 扩展显示 **hstring** 的字段。 显示的最后一项是字符串本身。

```dbgcmd
!hstring Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*地址*  
**HSTRING** 的地址。

<a name="remarks"></a>备注
-------

**HSTRING** 数据类型支持嵌入了空字符的字符串。 但是， **！ hstring** extension 只显示最多为第一个 NULL 字符的字符串。 若要查看包含嵌入的 NULL 字符的整个字符串，请使用 [**！ hstring2**](-hstring2.md) 扩展名。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[Windows 运行时调试程序命令](windows-runtime-debugger-commands.md)

[**!hstring2**](-hstring2.md)

[**!winrterr**](-winrterr.md)

 

 






