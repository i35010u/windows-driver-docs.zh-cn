---
title: 在各种状态之间切换的笔记本电脑/平板电脑模式
description: 本主题包含用于切换笔记本电脑/石板模式指示器状态的示例代码。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d3d8137469dbcdfc95aa5eb754f9a14612f75cf
ms.sourcegitcommit: 2a27786ed72024f064bbfef20933b0d0b429d4b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105106163"
---
# <a name="laptopslate-mode-toggling-between-states"></a>在各种状态之间切换的笔记本电脑/平板电脑模式


本主题包含用于切换笔记本电脑/石板模式指示器状态的示例代码。

```cpp
int __cdecl ToggleConversionIndicator(
    __in int argc,
    __in_ecount(argc) char **argv)
{
    LPWSTR DevicePath;
    HANDLE FileHandle;
    BOOL b;
    BYTE buffer;
    HWND hwnd;
    MSG msg;

//assuming our GetDevicePath method is creating a device path using use SetupDi API
    DevicePath = GetDevicePath((LPGUID)&GUID_GPIOBUTTONS_LAPTOPSLATE_INTERFACE);
   
    FileHandle = CreateFile(DevicePath,
                            GENERIC_WRITE,
                            0,
                            NULL,
                            OPEN_EXISTING,
                            0,
                            NULL);
   
    buffer = 0;
    WriteFile(FileHandle, &buffer, sizeof(buffer), NULL, NULL);

    return 0;
}
```

<b>注意：</b> 笔记本电脑/石板模式指示器设备一次只能由一个进程打开。 当另一个进程已打开设备时，CreateFile 将失败，并且 GetLastError 将返回 ERROR_ACCESS_DENIED。 

 




