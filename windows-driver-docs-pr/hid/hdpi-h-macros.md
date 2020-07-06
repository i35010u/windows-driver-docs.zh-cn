---
title: Hdpi.h 宏
description: Hdpi 标头中包含的宏。
ms.localizationpriority: medium
ms.date: 02/25/2020
ms.openlocfilehash: 1ebc9dfad8c16a77bddfd3d2043bf2ca06e81050
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968216"
---
# <a name="hdpih-macros"></a>Hdpi.h 宏

[Hdpi](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)头文件包含以下宏：

- [HidP \_ GetButtons](#hidp_getbuttons)
- [HidP \_ GetButtonsEx](#hidp_getbuttonsex)
- [HidP \_ SetButtons](#hidp_setbuttons)
- [HidP \_ UnsetButtons](#hidp_unsetbuttons)

## <a name="hidp_getbuttons"></a>HidP \_ GetButtons

**HidP \_ GetButtons**宏是[**HidP \_ GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)例程的助记键别名。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_getbuttonsex"></a>HidP \_ GetButtonsEx

**HidP \_ GetButtonsEx**宏是[**HidP \_ GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)例程的助记键别名。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_setbuttons"></a>HidP \_ SetButtons

**HidP \_ SetButtons**宏是[**HidP \_ SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)例程的助记键别名。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

## <a name="hidp_unsetbuttons"></a>HidP \_ UnsetButtons

**HidP \_ UnsetButtons**宏是[**HidP \_ UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)例程的助记键别名。

```cpp
#define HidP_UnsetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_UnsetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

### <a name="requirements"></a>要求

**标头**： [Hidpi](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/) （包括 hidpi）


## <a name="see-also"></a>另请参阅

[hidpi](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/)

[HidP \_ GetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)

[HidP \_ GetUsagesEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)

[HidP \_ SetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)

[HidP \_ UnsetUsages](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)
