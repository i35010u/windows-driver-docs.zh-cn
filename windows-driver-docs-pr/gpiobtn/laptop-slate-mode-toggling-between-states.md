---
title: 在各种状态之间切换的笔记本电脑/平板电脑模式
description: 本主题包含切换的便携式计算机/盖板模式指示器状态的示例代码。
ms.assetid: C5D9B586-EED7-4DC7-8BFF-3AB3A972307D
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e35e21cb956921d870384b8aa76a08a201b518ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344595"
---
# <a name="laptopslate-mode-toggling-between-states"></a>在各种状态之间切换的笔记本电脑/平板电脑模式


本主题包含切换的便携式计算机/盖板模式指示器状态的示例代码。

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
    DevicePath = GetDevicePath((LPGUID)&amp;GUID_GPIOBUTTONS_LAPTOPSLATE_INTERFACE);
   
    FileHandle = CreateFile(DevicePath,
                            GENERIC_WRITE,
                            0,
                            NULL,
                            OPEN_EXISTING,
                            0,
                            NULL);
   
    buffer = 0;
    WriteFile(FileHandle, &amp;buffer, sizeof(buffer), NULL, NULL);

    return 0;
}
```

 

 




