---
title: 在各种状态之间切换的笔记本电脑/平板电脑模式
description: 本主题包含用于切换笔记本电脑/石板模式指示器状态的示例代码。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 75bc3edd36a54137ecfd5375827bcf2ae2ba02ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830597"
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

 

 




