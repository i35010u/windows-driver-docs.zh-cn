---
title: 64 位操作系统上的反交错
description: 64 位操作系统上的反交错
ms.assetid: ffac0c1a-2c92-4beb-9622-26d10e1a06aa
keywords:
- 取消隔行扫描 WDK DirectX VA，64位
- 64位 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc0f1144b43991a7f85e26ff23826597c3221310
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063940"
---
# <a name="deinterlacing-on-64-bit-operating-systems"></a>64 位操作系统上的反交错


为了确保32位应用程序启动的取消隔行扫描操作在64位操作系统上成功运行，显示驱动程序代码必须首先检测应用程序是32位还是64位。 若要执行检测，驱动程序应检查应用程序通过的[**DXVA \_ DeinterlaceBlt**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)结构的**大小**成员。 32位版本的 DXVA \_ DeinterlaceBlt 小于64位版本的大小，因为指针大小介于32位和64位之间。 如果驱动程序确定初始应用程序为32位，则驱动程序应通过 thunk 处理取消隔行扫描操作。 有关 thunk 的详细信息，请参阅 [64 位驱动程序中的支持32位 i/o](../kernel/supporting-32-bit-i-o-in-your-64-bit-driver.md)。

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

 

