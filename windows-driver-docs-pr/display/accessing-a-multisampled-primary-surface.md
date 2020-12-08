---
title: 访问多重采样主图面
description: 访问多重采样主图面
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多级显示，访问主要图面
- 以多级显示方式呈现 WDK DirectX 8.0，访问主要图面
- 呈现 multisamples WDK DirectX 8.0，访问主要图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 127e18fbd7cdd135bc1c120ffc980806360f1b12
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810569"
---
# <a name="accessing-a-multisampled-primary-surface"></a>访问多重采样主图面


## <span id="ddk_accessing_a_multisampled_primary_surface_gg"></span><span id="DDK_ACCESSING_A_MULTISAMPLED_PRIMARY_SURFACE_GG"></span>


Direct3D 运行时阻止高性能 CPU 访问多级采样缓冲区。 但是，运行时可能会调用驱动程序的 [*DdLock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) 函数，以实现对多级采样缓冲区的低性能访问，例如在测试方案中用于屏幕截图和图像验证。

由于运行时无法处理多级采样缓冲区的示例布局，因此驱动程序必须转换格式，驱动程序的 [*DdLock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) 函数必须返回包含主图面的内容的数据缓冲区，该缓冲区以单个每像素样本格式显示。 如果应用程序调用 IDirect3DDevice8：： GetFrontBuffer 以获取多级采样翻转链的前台缓冲区的副本，Direct3D 运行时将调用该驱动程序的 *DdLock* 函数来锁定前台缓冲区。 此缓冲区包含当前前台缓冲区的一个版本，该版本解析为主要图面的名义宽度、高度和像素格式。

如果设备内存中提供了此类缓冲区，则驱动程序可以返回指向该缓冲区的指针。 如果此类缓冲区在设备内存中不可用 (与在扫描时) 解析采样时缓冲区的设备的情况相同，则驱动程序应在系统内存中分配一个缓冲区，并将多级采样前台缓冲区解析为此系统缓冲区。 运行时允许驱动程序根据需要花费很多时间将多级采样前台缓冲区解析到此系统缓冲区。

无论运行时在 \_ 调用驱动程序的 [*DDLOCK*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) 函数时是否设置 DDLOCK READONLY 标志，运行时都将这些缓冲区视为只读。 因此，无需驱动程序将任何数据从系统内存表面复制回设备内存。 此外，不需要驱动程序的 [*DdUnlock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock) 函数将单个每像素样本格式转换回主要图面的多级采样格式。

应用程序调用 **IDirect3DDevice8** 接口的 cursor 方法还可导致 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 调用以多级采样主要目标为目标。 这些 *DdBlt* 调用必须处理从单个像素样本游标数据到多级采样主数据的转换。

有关 **IDirect3DDevice8** 的详细信息，请参阅 DIRECTX 8.0 SDK 文档。

 

