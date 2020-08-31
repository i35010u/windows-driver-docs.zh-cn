---
title: Windows 显示驱动程序模型 (WDDM) 64 位问题
description: Windows 显示驱动程序模型 (WDDM) 64 位问题
ms.assetid: ab391fca-bc98-4e98-9531-7a1d24ee173d
keywords:
- 64位 WDK 显示
- 显示驱动程序模型 WDK Windows Vista，64位
- Windows Vista 显示器驱动程序型号 WDK，64位
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e85b0fb4df5c12b218d72331e997624984e9805
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063532"
---
# <a name="windows-display-driver-model-wddm-64-bit-issues"></a>Windows 显示驱动程序模型 (WDDM) 64 位问题


若要允许32位应用程序在64位操作系统上运行，除了需要64位应用程序需要的64位用户模式显示驱动程序外，还必须提供一个32位用户模式显示驱动程序。 但是，64位操作系统只需要64位版本的显示微型端口驱动程序。 Windows 上的 windows (WOW64) 使32位应用程序能够在64位操作系统上运行。 有关详细信息，请参阅 [64 位驱动程序中的支持32位 i/o](../kernel/supporting-32-bit-i-o-in-your-64-bit-driver.md)。

若要在64位操作系统上安装32位用户模式显示驱动程序，必须在图形设备的显示微型端口驱动程序的 INF 文件的 "外接程序" 部分中设置以下项。 这必须发生，以便在驱动程序安装过程中将32位用户模式显示驱动程序的 DLL 名称添加到注册表中：

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverNameWow, %REG_MULTI_SZ%, Xxx.dll
...
```

INF 文件必须包含信息，以指示操作系统将32位用户模式显示驱动程序复制到系统的% systemroot% \\ SysWOW64 目录。 有关详细信息，请参阅 [**Inf CopyFiles 指令**](../install/inf-copyfiles-directive.md) 和 [**inf DestinationDirs 部分**](../install/inf-destinationdirs-section.md)。

由于 WOW64 无法处理不透明或非类型化的数据结构，例如通过[**pfnAllocateCb**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数传递的[**D3DDDICB \_ 分配**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)结构，因此它无法执行从32位到64位的自动转换。 因此，要使 WOW64 正常工作，在将32位用户模式显示驱动程序写入到64位操作系统上运行时，必须考虑以下各项：

-   避免指向多个操作系统（如大小为 \_ T 或句柄）的敏感指针或数据类型。 除了设置整个结构变量的大小以外，这些可变宽度数据类型使各个成员的对齐和位置不同。 如果可变宽度成员是不可避免的，你可以添加另一个成员，以指示该数据结构源自32位用户模式显示驱动程序。 然后，64位显示微型端口驱动程序可以正确执行转换。

-   即使不存在可变宽度成员，您也可能需要考虑特定于体系结构的对齐要求。 例如，在 x64 上，UINT64 (或 QWORD) 应为8字节对齐。 由于标准32位编译器编译的32位用户模式显示驱动程序可能不会正确对齐这些本机64位类型，因此，64位显示微型端口驱动程序可能无法从32位用户模式显示驱动程序中精确地访问数据。 但是，您可以通过使用相应的 **杂注** 编译器指令来强制对齐。 尽管使用 **杂注** 编译器指令可能会导致在32位操作系统上稍微浪费空间，但这使你可以在32位和64位操作系统上使用相同的32位用户模式显示驱动程序。 如果无法通过使用合适的 **pragma** 编译器指令来强制对齐，则在64位操作系统上使用 WOW64 运行的32位用户模式显示驱动程序必须与在32位操作系统上运行的32位用户模式显示驱动程序不同。

 

