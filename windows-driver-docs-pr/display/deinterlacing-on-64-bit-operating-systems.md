---
title: 64 位操作系统上的反交错
description: 64 位操作系统上的反交错
ms.assetid: ffac0c1a-2c92-4beb-9622-26d10e1a06aa
keywords:
- 取消隔行扫描 WDK DirectX VA，64位
- 64位 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274d881b36689f6d2f0d89a88b8af43868e37a39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839758"
---
# <a name="deinterlacing-on-64-bit-operating-systems"></a>64 位操作系统上的反交错


为了确保32位应用程序启动的取消隔行扫描操作在64位操作系统上成功运行，显示驱动程序代码必须首先检测应用程序是32位还是64位。 若要执行检测，驱动程序应检查应用程序通过的[**DXVA\_DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlaceblt)结构的**大小**成员。 32位版本的 DXVA\_DeinterlaceBlt 小于64位版本的大小，因为指针大小在32位与64位之间存在差异。 如果驱动程序确定初始应用程序为32位，则驱动程序应通过 thunk 处理取消隔行扫描操作。 有关 thunk 的详细信息，请参阅[64 位驱动程序中的支持32位 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)。

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

 

 





