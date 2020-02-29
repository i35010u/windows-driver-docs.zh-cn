---
title: Hdpi.h 宏
description: Hdpi 标头中包含的宏。
ms.localizationpriority: medium
ms.date: 02/25/2020
ms.openlocfilehash: a781f092f31abf5be80d82c6a77557aeed0acb46
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166683"
---
# <a name="hdpih-macros"></a>Hdpi.h 宏

[Hdpi](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)头文件包含以下宏：

- [HidP\_GetButtons](#hidp_getbuttons)
- [HidP\_GetButtonsEx](#hidp_getbuttonsex)
- [HidP\_SetButtons](#hidp_setbuttons)
- [HidP\_UnsetButtons](#hidp_unsetbuttons)

## <a name="hidp_getbuttons"></a>HidP\_GetButtons

**HidP\_GetButtons**宏是[**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)例程的助记键别名。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_getbuttonsex"></a>HidP\_GetButtonsEx

**HidP\_GetButtonsEx**宏是[**HidP\_GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)例程的助记键别名。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_setbuttons"></a>HidP\_SetButtons

**HidP\_SetButtons**宏是[**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)例程的助记键别名。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

## <a name="hidp_unsetbuttons"></a>HidP\_UnsetButtons

**HidP\_UnsetButtons**宏是[**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)例程的助记键别名。

```cpp
#define HidP_UnsetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_UnsetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

### <a name="requirements"></a>要求

| | |
| --- | --- |
| 标头 | [hidpi](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/) （包括 hidpi） |

## <a name="see-also"></a>另请参阅

[hidpi](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)

[HidP\_GetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)

[HidP\_GetUsagesEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)

[HidP\_SetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)

[HidP\_UnsetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
