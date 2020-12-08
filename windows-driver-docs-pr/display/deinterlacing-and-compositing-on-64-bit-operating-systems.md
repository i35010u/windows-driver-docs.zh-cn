---
title: 在 64 位操作系统上进行反交错与合成
description: 在 64 位操作系统上进行反交错与合成
keywords:
- 取消隔行扫描 WDK DirectX VA，64位
- 64位 WDK DirectX VA
- DXVA_DeinterlaceBltEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02c839d96950e8427c922f0657180ed27f50f86
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809575"
---
# <a name="deinterlacing-and-compositing-on-64-bit-operating-systems"></a>在 64 位操作系统上进行反交错与合成


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

为了确保由32位应用程序启动的子 [流组合操作的取消隔行扫描](performing-deinterlacing-with-substream-compositing-operations.md) 在64位操作系统上成功运行，显示驱动程序代码必须首先检测应用程序是32位还是64位。 若要执行检测，驱动程序应检查应用程序通过的 [**DXVA \_ DeinterlaceBltEx**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex) 结构的大小。 如果驱动程序确定初始应用程序为32位，则驱动程序应通过 thunk 处理取消隔行扫描操作。 驱动程序应使用 [**DXVA \_ VideoSample32**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample32) 和 [**DXVA \_ DeinterlaceBltEx32**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex32) 结构来执行隔行扫描 thunk。 有关 thunk 的详细信息，请参阅 [64 位驱动程序中的支持32位 i/o](../kernel/supporting-32-bit-i-o-in-your-64-bit-driver.md)。

**注意**   如果为64位编译了驱动程序代码，则 [**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2) 结构将包含两个额外的 DWORD 成员，以使32位版本的 DXVA VideoSample2 的大小与 \_ 64 位版本不同。 由于有8个字节的对齐方式，32位编译器会向32位版本的末尾添加4个字节的填充，这就不需要这两个额外的 DWORD 成员--使32位版本与64该版本的版本相同，甚至还考虑到指针大小在32与64位之间的差异。
如果 DXVA VideoSample2 中包含两个额外 \_ 的 DWORD 成员用于64位编译，则驱动程序可以根据 [**DXVA \_ DeinterlaceBltEx**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)结构的 **大小** 成员来区分32位和64位版本。

 

下面的示例代码演示了驱动程序应如何处理 thunk：

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

 

