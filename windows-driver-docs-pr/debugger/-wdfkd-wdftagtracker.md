---
title: wdfkd.wdftagtracker
description: Wdfkd.wdftagtracker 扩展指定的标记跟踪器显示所有可用的标记信息 （包括标记值、 行、 文件和时间）。
ms.assetid: d8720446-58c1-4792-9e16-0facfe8fa39f
keywords:
- wdfkd.wdftagtracker Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftagtracker
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53ebbd9d25c65adf13f5bbbb0edaa801cd452a23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323265"
---
# <a name="wdfkdwdftagtracker"></a>!wdfkd.wdftagtracker


**！ Wdfkd.wdftagtracker**扩展指定的标记跟踪器将显示所有可用的标记信息 （包括标记值、 行、 文件和时间）。

```dbgcmd
!wdfkd.wdftagtracker TagObjectPointer [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______TagObjectPointer______"></span><span id="_______tagobjectpointer______"></span><span id="_______TAGOBJECTPOINTER______"></span> *TagObjectPointer*   
指向标记跟踪器的指针。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 要显示的信息类型。 *标志*可以是以下位的任意组合。 默认值为 0x0。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示历史记录获取操作和释放对象上的操作。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
以十六进制格式而不是小数显示的对象的行号。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>框架

KMDF 1，UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

若要检索一个指向标记跟踪器，请使用[ **！ wdfkd.wdfobject** ](-wdfkd-wdfobject.md)内部框架对象指针上的扩展。

若要使用跟踪标记，必须启用内核模式驱动程序框架 (KMDF) 验证程序，并处理跟踪在注册表中。 这两个设置都存储在驱动程序的**参数\\Wdf**的子项**HKEY\_本地\_机\\系统\\CurrentControlSet\\Services**密钥。

若要启用 KMDF 验证工具，请将设置为非零值**VerifierOn**。

若要跟踪的句柄，设置的值**TrackHandles**到一个或多个对象类型的名称或指定一个星号 (\*) 用于跟踪所有对象类型。 例如，下面的示例指定对所有 WDFDEVICE 和 WDFQUEUE 对象的引用的跟踪。

```text
TrackHandles: MULTI_SZ: WDFDEVICE WDFQUEUE
```

启用跟踪的对象类型的句柄时，框架将跟踪的引用，该类型的任何对象上执行。 此设置可在查找未释放的引用会导致驱动程序内存泄漏。 **TrackHandles**仅适用于 KMDF 验证程序已启用。

 

 





