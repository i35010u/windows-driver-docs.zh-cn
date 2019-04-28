---
title: hstring
description: Hstring 扩展显示 HSTRING 的字段。 在显示中的最后一项是字符串本身。
ms.assetid: 6FB85609-0FB1-457E-A58E-804F69016406
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
ms.openlocfilehash: 8c41b63cde736165acf39cf9554be488c0bffbb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336458"
---
# <a name="hstring"></a>!hstring


**！ Hstring**扩展显示的字段**HSTRING**。 在显示中的最后一项是字符串本身。

```dbgcmd
!hstring Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*Address*  
地址**HSTRING**。

<a name="remarks"></a>备注
-------

**HSTRING**数据类型支持有嵌入的 NULL 字符的字符串。 但是， **！ hstring**扩展显示仅第一个空字符之前的字符串。 若要查看整个字符串包含嵌入的 NULL 字符，请使用[ **！ hstring2** ](-hstring2.md)扩展。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[Windows 运行时调试器命令](windows-runtime-debugger-commands.md)

[**!hstring2**](-hstring2.md)

[**!winrterr**](-winrterr.md)

 

 






