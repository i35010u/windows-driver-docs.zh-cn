---
title: Hdpi.h 宏
description: Hdpi.h 标头中包含的宏。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3dbbc0c8d237e3b1cc9d5b6e787bcd79db03bd3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388906"
---
# <a name="hdpih-macros"></a>Hdpi.h 宏

Hdpi.h 标头文件包含几个宏。 本主题介绍以下宏：

* [**HidP\_GetButtons**](#HidPGetButtons)
* [**HidP\_GetButtonsEx**](#HidPGetButtonsEx)
* [**HidP\_SetButtons**](#HidPSetButtons)
* [**HidP\_UnsetButtons**](#HidPUnsetButtons)


##  <a name="hidpgetbuttons"></a>HidP\_GetButtons


**HidP\_GetButtons**宏是的助记键别名[ **HidP\_GetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539742)例程。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

##  <a name="hidpgetbuttonsex"></a>HidP\_GetButtonsEx


**HidP\_GetButtonsEx**宏是一个助记键别名[ **HidP\_GetUsagesEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539745)例程。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```


##  <a name="hidpsetbuttons"></a>HidP\_SetButtons


**HidP\_SetButtons**宏是的助记键别名[ **HidP\_SetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539792)例程。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

##  <a name="hidpunsetbuttons"></a>HidP\_UnsetButtons


**HidP\_UnsetButtons**宏是的助记键别名[ **HidP\_UnsetUsages** ](https://msdn.microsoft.com/library/windows/hardware/ff539819)例程。

```cpp
#define HidP_UnsetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_UnsetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hidpi.h （包括 Hidpi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**HidP\_GetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539742)

[**HidP\_GetUsagesEx**](https://msdn.microsoft.com/library/windows/hardware/ff539745)

[**HidP\_SetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539792)

[**HidP\_UnsetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539819)






