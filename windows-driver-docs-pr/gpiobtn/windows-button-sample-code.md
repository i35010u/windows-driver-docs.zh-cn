---
title: Windows 按钮示例代码
description: 本主题包含一个代码示例，该示例将已标识的 Windows 按钮向下和向上切换。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 33b808965a2298a6fb0f8e8c99d9d300503edcb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783941"
---
# <a name="windows-button-sample-code"></a>Windows 按钮示例代码


本主题包含一个代码示例，该示例将已标识的 Windows 按钮向下和向上切换。

```cpp
int __cdecl InjectButtonPress(
    __in int argc,
    __in_ecount(argc) char **argv)
{
    LPWSTR DevicePath;
    HANDLE FileHandle;
    BOOL b;
    BYTE buffer;
    HWND hwnd;
    MSG msg;

    DevicePath = GetDevicePath((LPGUID)&GUID_GPIOBUTTONS_NOTIFY_INTERFACE);

    FileHandle = CreateFile(DevicePath,
                            GENERIC_WRITE,
                            0,
                            NULL,
                            OPEN_EXISTING,
                            0,
                            NULL);
   
    buffer = GPIO_BUTTON_WINDOWS; //using GPIOBUTTONS_BUTTON_TYPE enum defined above
    WriteFile(FileHandle, &buffer, sizeof(buffer), NULL, NULL); // send button down
    buffer = GPIO_BUTTON_WINDOWS;
    WriteFile(FileHandle, &buffer, sizeof(buffer), NULL, NULL); // send button up

    return 0;
}
```

 

 




