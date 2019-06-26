---
title: Hdpi.h 宏
description: Hdpi.h 标头中包含的宏。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9c3436cd937f900966a33c781d3455e05ebcdbd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360869"
---
# <a name="hdpih-macros"></a>Hdpi.h 宏

Hdpi.h 标头文件包含几个宏。 本主题介绍以下宏：

* [**HidP\_GetButtons**](#hidp_getbuttons)
* [**HidP\_GetButtonsEx**](#hidp_getbuttonsex)
* [**HidP\_SetButtons**](#hidp_setbuttons)
* [**HidP\_UnsetButtons**](#hidp_unsetbuttons)


##  <a name="hidp_getbuttons"></a>HidP\_GetButtons


**HidP\_GetButtons**宏是的助记键别名[ **HidP\_GetUsages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusages)例程。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

##  <a name="hidp_getbuttonsex"></a>HidP\_GetButtonsEx


**HidP\_GetButtonsEx**宏是一个助记键别名[ **HidP\_GetUsagesEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagesex)例程。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```


##  <a name="hidp_setbuttons"></a>HidP\_SetButtons


**HidP\_SetButtons**宏是的助记键别名[ **HidP\_SetUsages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusages)例程。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

##  <a name="hidp_unsetbuttons"></a>HidP\_UnsetButtons


**HidP\_UnsetButtons**宏是的助记键别名[ **HidP\_UnsetUsages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_unsetusages)例程。

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

[**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusages)

[**HidP\_GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagesex)

[**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusages)

[**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_unsetusages)






