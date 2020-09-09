---
title: Hdpi.h 宏
description: Hdpi 标头中包含的宏。
ms.localizationpriority: medium
ms.date: 02/25/2020
ms.openlocfilehash: a51d42f7097c7539a050a3884c7c67b9323c4787
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592409"
---
# <a name="hdpih-macros"></a>Hdpi.h 宏

[Hdpi](/windows-hardware/drivers/ddi/hidpi/)头文件包含以下宏：

- [HidP \_ GetButtons](#hidp_getbuttons)
- [HidP \_ GetButtonsEx](#hidp_getbuttonsex)
- [HidP \_ SetButtons](#hidp_setbuttons)
- [HidP \_ UnsetButtons](#hidp_unsetbuttons)

## <a name="hidp_getbuttons"></a>HidP \_ GetButtons

**HidP \_ GetButtons**宏是[**HidP \_ GetUsages**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)例程的助记键别名。

```cpp
#define HidP_GetButtons(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe) \
        HidP_GetUsages(Rty, UPa, LCo, ULi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_getbuttonsex"></a>HidP \_ GetButtonsEx

**HidP \_ GetButtonsEx**宏是[**HidP \_ GetUsagesEx**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)例程的助记键别名。

```cpp
#define HidP_GetButtonsEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)  \
         HidP_GetUsagesEx(Rty, LCo, BLi, ULe, Ppd, Rep, RLe)
```

## <a name="hidp_setbuttons"></a>HidP \_ SetButtons

**HidP \_ SetButtons**宏是[**HidP \_ SetUsages**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)例程的助记键别名。

```cpp
#define HidP_SetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_SetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

## <a name="hidp_unsetbuttons"></a>HidP \_ UnsetButtons

**HidP \_ UnsetButtons**宏是[**HidP \_ UnsetUsages**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)例程的助记键别名。

```cpp
#define HidP_UnsetButtons(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle) \
        HidP_UnsetUsages(Rty, Up, Lco, ULi, ULe, Ppd, Rep, Rle)
```

### <a name="requirements"></a>要求

**标头**： [Hidpi](/windows-hardware/drivers/ddi/hidpi/) (包含 hidpi) 


## <a name="see-also"></a>另请参阅

[hidpi](/windows-hardware/drivers/ddi/hidpi/)

[HidP \_ GetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)

[HidP \_ GetUsagesEx](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)

[HidP \_ SetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)

[HidP \_ UnsetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)