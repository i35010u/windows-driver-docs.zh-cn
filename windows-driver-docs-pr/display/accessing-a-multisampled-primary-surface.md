---
title: 访问多重采样主图面
description: 访问多重采样主图面
ms.assetid: 5d83699c-45ae-46d1-8804-1a18bfbc203f
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多重采样呈现、 访问主图面
- multisample 呈现 WDK DirectX 8.0、 访问主图面
- 呈现 multisamples WDK DirectX 8.0，访问主图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4727dbc6abfb2807c7e1628eb4870ce523046c96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375402"
---
# <a name="accessing-a-multisampled-primary-surface"></a>访问多重采样主图面


## <span id="ddk_accessing_a_multisampled_primary_surface_gg"></span><span id="DDK_ACCESSING_A_MULTISAMPLED_PRIMARY_SURFACE_GG"></span>


Direct3D 运行时禁止对多级采样缓冲区的高性能 CPU 访问。 但是，在运行时可能会调用的驱动程序[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)屏幕快照和映像验证在测试方案中性能较低访问多级采样缓冲区，例如函数。

由于运行时不能处理的多级采样缓冲区示例布局，该驱动程序必须转换格式，并在驱动程序[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)函数必须返回包含的数据的缓冲区在主面以一种示例每像素格式的内容。 如果应用程序调用 IDirect3DDevice8::GetFrontBuffer 以获取多级采样翻转链在前台缓冲区的副本，Direct3D 运行时调用的驱动程序*DdLock*函数来锁定前台缓冲区。 此缓冲区包含当前被解析到的主表面名义上的宽度、 高度和像素格式的前台缓冲区的版本。

如果此类缓冲区中设备内存可用，则驱动程序可以向该缓冲区返回一个指针。 如果此类缓冲区不可用在设备内存中 （像在扫描扩展时解析多级采样缓冲区的设备的情况一样），则该驱动程序应分配在系统内存中的缓冲区并解析多级采样的前缓冲，为此系统缓冲区。 运行时允许驱动程序需要解析多级采样的前缓冲，为此系统缓冲区所需的足够的时间。

无论是否在运行时设置 DDLOCK\_时它会调用驱动程序的只读标志[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)函数，这些缓冲区为只读模式运行时处理。 因此，该驱动程序不需要复制任何系统内存中的数据呈现回设备内存。 另外，该驱动程序[ *DdUnlock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)函数不需要将单个示例每像素格式转换回主表面多级采样格式。

对游标方法的应用程序通过调用**IDirect3DDevice8**接口还可能会导致[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)面向多级采样的主数据库的调用。 这些*DdBlt*调用必须处理从单示例每像素光标数据到多级采样的主副本的转换。

有关详细信息**IDirect3DDevice8**，请参阅 DirectX 8.0 SDK 文档。

 

 





