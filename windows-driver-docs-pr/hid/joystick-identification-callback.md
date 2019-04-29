---
title: 游戏杆标识回调
description: 游戏杆标识回调
ms.assetid: d5e859d2-bfe4-41ef-9d09-ebb945d299bd
keywords:
- 回调 WDK 游戏杆
- WDK HID 游戏杆、 请求 ID
- ID 请求 WDK 游戏杆
- 标识回叫 WDK 游戏杆
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 209d6b25b3d9494f1566e00df1b698bcf4de5c7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355341"
---
# <a name="joystick-identification-callback"></a>游戏杆标识回调





```cpp
int __stdcall JoyIdRoutine( int joyid, BOOL used );
```

VJoyD 调用 JoyIDRoutine 时用户配置或取消配置作为一个 16 游戏杆游戏杆。 如果微型驱动程序可以支持中所请求的 ID *joyid*，JoyIdRoutine 返回非零值。 如果微型驱动程序不能支持 ID，则例程将返回零值。

每当进行任何更改，joyConfigChanged 调用以更新的驱动程序，VJoyD 循环访问所有 16 台设备，从 JOYSTICKID1 开始。 它将所有设备重都置为未使用，然后循环访问它们，以便将所有这些系统需要使用的设置。 控件面板在操作期间，此过程可以需要大量的调用，用于初始化此回调用法中创建问题。 这是如果在系统启动完成之前进行调用，这是其他服务不可用时尤其如此。

多个设备的服务回调应尝试保留游戏杆标识符的微型驱动程序绑定到单一物理设备时，如果可能，避免用户混淆。 您可以实现这相对轻松地在单个会话中，但可能是没有必要通过重新启动。

 

 




