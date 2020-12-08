---
title: 可用接口和相关 API
description: 每个设备有三个 GPIO 接口。 每个接口都由一个 GUID 引用。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9a0a98afabf5ea052ab72aaca14ccdce38736382
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827193"
---
# <a name="available-interfaces-and-related-apis"></a>可用接口和相关 API


有三种 GPIO 接口：每个设备一个。 每个接口都由一个 GUID 引用。

/\* 30ebfbf8-df5f-4d4d-9fc5-a26c7fd1df4a \* /DEFINE \_ GUID (guid \_ GPIOBUTTONS \_ NOTIFY \_ INTERFACE，0x30ebfbf8，0xdf5f，0x4d4d，0x9f，0xc5，0xa2，0x6c，0x7f，0xd1，0xdf，0x4a) ;

/\* 317fc439-3f77-41c8-b09e-08ad63272aa3 \* /DEFINE \_ GUID (guid \_ GPIOBUTTONS \_ LAPTOPSLATE \_ INTERFACE、0x317fc439、0x3f77、0x41c8、0xb0、0x9e、0x08、0xad、0x63、0x27、0x2a、0xa3) ;

/\* a84e689b-0dce-493a-a164-acde05478fc3 \* /DEFINE \_ GUID (guid \_ GPIOBUTTONS \_ DOCKMODE \_ INTERFACE、0xa84e689b、0x0dce、0x493a、0xa1、0x64、0xac、0xde、0x05、0x47、0x8f、0xc3) ;

接口允许通过针对各自的设备接口调用 WriteFile 来切换按钮或指示器的状态。

**注意**  
若要防止多个提供程序之间发生潜在的冲突，设备的句柄提供对设备的独占访问权限。

 

``` syntax
typedef enum {
    GPIO_BUTTON_POWER,
    GPIO_BUTTON_WINDOWS,
    GPIO_BUTTON_VOLUME_UP,
    GPIO_BUTTON_VOLUME_DOWN,
    GPIO_BUTTON_ROTATION_LOCK,
} GPIOBUTTONS_BUTTON_TYPE;
```

 

 




