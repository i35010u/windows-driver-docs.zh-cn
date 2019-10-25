---
title: Hdpi.h 宏
description: Hdpi 标头中包含的宏。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3181026688e74ab47a1fb479712b84fde16c99d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824813"
---
# <a name="hdpih-macros"></a>Hdpi.h 宏

Hdpi 头文件包含多个宏。 本主题介绍以下宏：

* [**HidP\_GetButtons**](#hidp_getbuttons)
* [**HidP\_GetButtonsEx**](#hidp_getbuttonsex)
* [**HidP\_SetButtons**](#hidp_setbuttons)
* [**HidP\_UnsetButtons**](#hidp_unsetbuttons)


##  <a name="hidp_getbuttons"></a>HidP\_GetButtons


**HidP\_GetButtons**宏是[**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)例程的助记键别名。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

##  <a name="hidp_getbuttonsex"></a>HidP\_GetButtonsEx


**HidP\_GetButtonsEx**宏是[**HidP\_GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)例程的助记键别名。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```


##  <a name="hidp_setbuttons"></a>HidP\_SetButtons


**HidP\_SetButtons**宏是[**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)例程的助记键别名。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

##  <a name="hidp_unsetbuttons"></a>HidP\_UnsetButtons


**HidP\_UnsetButtons**宏是[**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)例程的助记键别名。

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
<td><p>标头</p></td>
<td>Hidpi （包括 Hidpi）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)

[**HidP\_GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)

[**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)

[**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)






