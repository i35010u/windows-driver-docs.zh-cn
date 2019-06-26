---
title: 在 64 位操作系统上进行反交错与合成
description: 在 64 位操作系统上进行反交错与合成
ms.assetid: af95b9f8-1329-4cba-a70f-4f1884f6a0f9
keywords:
- 取消隔行扫描 WDK DirectX VA，64年位
- 64 位 WDK DirectX VA
- DXVA_DeinterlaceBltEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a60298b1d27b8a885f9a02124b5d8809b3a58d5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384901"
---
# <a name="deinterlacing-and-compositing-on-64-bit-operating-systems"></a>在 64 位操作系统上进行反交错与合成


本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。

若要确保[与子流合成操作去隔行](performing-deinterlacing-with-substream-compositing-operations.md)启动 64 位操作系统上成功运行的 32 位应用程序，显示驱动程序代码必须首先检测应用程序是 32 位或 64位。 若要执行检测，该驱动程序应检查的大小[ **DXVA\_DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)应用程序传递的结构。 如果该驱动程序确定起始应用程序是 32 位，该驱动程序应处理取消隔行扫描操作的形式转换。 该驱动程序应使用[ **DXVA\_VideoSample32** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample32)并[ **DXVA\_DeinterlaceBltEx32** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex32)若要执行取消隔行扫描转换 （thunk） 的结构。 有关形式转换的详细信息，请参阅[在 64 位驱动程序中支持 32 位 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)。

**请注意**  驱动程序代码编译为 64 位时[ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)结构包含两个额外的 DWORD 成员，若要使 32 位的大小DXVA 版本\_VideoSample2 不同于 64 位版本。 8 字节对齐方式，由于 32 位编译器将 4 个字节填充添加到 32 位版本，这样-而无需这两个额外 DWORD 成员-32 位版本的指针大小差异的甚至记帐的 64 位版本的大小相同的端之间 32 位和 64 位。
具有两个额外的 DWORD 成员包含在 DXVA\_VideoSample2 64 位编译的该驱动程序可以区分基于 32 位和 64 位版本**大小**的成员[ **DXVA\_DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)结构。

 

下面的代码示例演示了该驱动程序应如何处理转换 （thunk）：

```cpp
switch (lpData->dwFunction) {
case DXVA_DeinterlaceBltExFnCode:
    {   DXVA_DeinterlaceBltEx* pBlt = (DXVA_DeinterlaceBltEx*)lpData->lpInputData; 
        switch (pBlt->Size) {
             case sizeof(DXVA_DeinterlaceBltEx): // should be 4400 bytes on Win64
                                                // should be 4144 bytes on Win32
                  break;
#ifdef _WIN64
             case sizeof(DXVA_DeinterlaceBltEx32): // should be 4144 bytes
                  // 32-bit structure, so thunk it!
                  break;
#endif
            default:
                  // unknown structure, so return error;
                  break;
            }
      }
```

 

 





