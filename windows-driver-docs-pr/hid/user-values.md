---
title: 用户的值
description: 用户的值
ms.assetid: 42b57fc2-fda0-464a-83dc-3e63ef693e9f
keywords:
- 用户的注册表设置 WDK 游戏杆
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6638a4e2950b19977b335563180713a70aa0e92b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376727"
---
# <a name="user-values"></a>用户的值





单个值名为 REGSTR\_VAL\_JOYUSERVALUES 存储如下所述的结构。 此结构指定如何数据应通过操作 VJoyD 当应用程序请求数据即可缩放居中显示，或已定义的死区域。

```cpp
struct {
    /* value at which to time-out internal joystick polling */
    DWORD   dwTimeOut;
 
    /* range of values app wants returned for axes */
    struct { 
        /* minimums for each axis */
        struct {
            DWORD    dwX;
            DWORD    dwY;
            DWORD    dwZ;
            DWORD    dwR;
            DWORD    dwU;
            DWORD    dwV;
        } jpMin;
        /* maximums for each axis */
        struct {
            DWORD    dwX;
            DWORD    dwY;
            DWORD    dwZ;
            DWORD    dwR;
            DWORD    dwU;
            DWORD    dwV;
        } jpMax;
        /* center positions for each axis */
        struct {
            DWORD    dwX;
            DWORD    dwY;
            DWORD    dwZ;
            DWORD    dwR;
            DWORD    dwU;
            DWORD    dwV;
        } jpCenter;
    } jrvRanges;
 
    /* area around center to be considered as "dead". specified as */
    /* a percentage (0-100). Only X & Y handled by system driver */
    struct {
        DWORD    dwX;
        DWORD    dwY;
        DWORD    dwZ;
        DWORD    dwR;
        DWORD    dwU;
        DWORD    dwV;
    } jpDeadZone;
}
```

 

 




