---
title: 64 位操作系统上的反交错
description: 64 位操作系统上的反交错
keywords:
- 取消隔行扫描 WDK DirectX VA，64位
- 64位 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86b7bb81ce55b08e5532678132a6ec5f21e7b05e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809563"
---
# <a name="deinterlacing-on-64-bit-operating-systems"></a>64 位操作系统上的反交错


为了确保32位应用程序启动的取消隔行扫描操作在64位操作系统上成功运行，显示驱动程序代码必须首先检测应用程序是32位还是64位。 若要执行检测，驱动程序应检查应用程序通过的 [**DXVA \_ DeinterlaceBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)结构的 **大小** 成员。 32位版本的 DXVA \_ DeinterlaceBlt 小于64位版本的大小，因为指针大小介于32位和64位之间。 如果驱动程序确定初始应用程序为32位，则驱动程序应通过 thunk 处理取消隔行扫描操作。 有关 thunk 的详细信息，请参阅 [64 位驱动程序中的支持32位 i/o](../kernel/supporting-32-bit-i-o-in-your-64-bit-driver.md)。

下面的示例代码演示了驱动程序应如何处理 thunk：

```cpp
switch (lpData->dwFunction) {
case DXVA_DeinterlaceBltFnCode:
    {   
        DXVA_DeinterlaceBlt* pBlt = (DXVA_DeinterlaceBlt*)lpData->lpInputData; 
         if (pBlt->Size == sizeof(DXVA_DeinterlaceBlt)) {
            // correctly formed 64-bit or 32-bit structure, so use it
        }
#ifdef _WIN64
        else if (pBlt->Size < sizeof(DXVA_DeinterlaceBlt)) {
            // 32-bit structure, so thunk it!
        }
#endif
        else {
            // unknown structure, so return error;
        }
    }
```

 

