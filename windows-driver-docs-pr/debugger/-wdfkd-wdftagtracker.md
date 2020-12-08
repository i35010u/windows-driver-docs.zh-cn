---
title: wdfkd.wdftagtracker
description: Wdfkd wdftagtracker 扩展显示 (包括指定标记跟踪器的标记值、行、文件和时间) 的所有可用标记信息。
keywords:
- wdfkd wdftagtracker Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftagtracker
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5210cd25748c69e9c18a86d8f92a124035d86740
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785303"
---
# <a name="wdfkdwdftagtracker"></a>!wdfkd.wdftagtracker


**！ Wdfkd wdftagtracker** 扩展显示 (包括指定标记跟踪器的标记值、行、文件和时间) 的所有可用标记信息。

```dbgcmd
!wdfkd.wdftagtracker TagObjectPointer [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______TagObjectPointer______"></span><span id="_______tagobjectpointer______"></span><span id="_______TAGOBJECTPOINTER______"></span>*TagObjectPointer*   
指向标记跟踪器的指针。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示对象上的获取操作和发布操作的历史记录。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
以十六进制而不是小数形式显示对象的行号。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

若要检索指向标记跟踪器的指针，请对内部框架对象指针使用 [**！ wdfkd**](-wdfkd-wdfobject.md) 扩展名。

若要使用标记跟踪，必须在注册表中同时启用 Kernel-Mode Driver Framework (KMDF) 验证器和处理跟踪。 这两个设置都存储在驱动程序的 **HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services** 项的 **参数 \\ Wdf** 子项中。

若要启用 KMDF 验证程序，请为 **VerifierOn** 设置非零值。

若要启用句柄跟踪，请将 **TrackHandles** 的值设置为一个或多个对象类型的名称，或指定星号 (\*) 以跟踪所有对象类型。 例如，下面的示例指定跟踪对所有 WDFDEVICE 和 WDFQUEUE 对象的引用。

```text
TrackHandles: MULTI_SZ: WDFDEVICE WDFQUEUE
```

启用对象类型的句柄跟踪后，框架将跟踪对该类型的任何对象所采用的引用。 此设置对于查找未发布引用原因的驱动程序内存泄漏很有用。 仅当启用了 KMDF verifier 时， **TrackHandles** 才有效。

 

 





