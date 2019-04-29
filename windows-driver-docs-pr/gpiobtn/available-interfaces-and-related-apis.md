---
title: 可用接口和相关 API
description: 有三个 GPIO 接口一个，每个设备。 每个接口的 guid 引用。
ms.assetid: 87A275B0-825A-47F1-9701-D7E91C493877
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1964a81972ae77c7034ae9d516437ab2f7b01274
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326116"
---
# <a name="available-interfaces-and-related-apis"></a>可用接口和相关 API


有三个 GPIO 接口： 一个用于每个设备。 每个接口的 guid 引用。

/\* 30ebfbf8-df5f-4d4d-9fc5-a26c7fd1df4a \*/define\_GUID (GUID\_GPIOBUTTONS\_通知\_接口，0x30ebfbf8、 0xdf5f、 0x4d4d、 0x9f 以及 0xc5 0xa2，、 0x6c、 0x7f，0xd1、 0xdf，0x4a);

/\* 317fc439-3f77-41c8-b09e-08ad63272aa3 \*/define\_GUID (GUID\_GPIOBUTTONS\_LAPTOPSLATE\_接口，0x317fc439、 0x3f77、 0x41c8、 0xb0，0x9e、 0x08，0xad、 0x63，0x27，0x2a，0xa3);

/\* a84e689b-0dce-493a-a164-acde05478fc3 \*/define\_GUID (GUID\_GPIOBUTTONS\_DOCKMODE\_接口，0xa84e689b、 0x0dce、 0x493a、 0xa1，0x64、 0xac，0xde、 0x05:sp，0x47、 0x8f，0xc3);

接口允许按钮或指示符以由针对相应设备接口调用 WriteFile 切换状态。

**请注意**  以防止多个提供程序之间的潜在冲突，该设备的句柄，提供了到设备的独占访问权限。

 

``` syntax
typedef enum {
    GPIO_BUTTON_POWER,
    GPIO_BUTTON_WINDOWS,
    GPIO_BUTTON_VOLUME_UP,
    GPIO_BUTTON_VOLUME_DOWN,
    GPIO_BUTTON_ROTATION_LOCK,
} GPIOBUTTONS_BUTTON_TYPE;
```

 

 




