---
title: 框架文件对象
description: 框架文件对象
ms.assetid: dd8215ee-2c10-4e49-9d7f-d2295bf219da
keywords:
- UMDF 对象 WDK，文件对象
- framework 对象 WDK UMDF，文件对象
- 文件对象 WDK UMDF
- IWDFFile
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3caa9e2080ec9843523ae8301ef4548c146db75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519225"
---
# <a name="framework-file-object"></a>框架文件对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架文件对象公开到由驱动程序[IWDFFile](https://msdn.microsoft.com/library/windows/hardware/ff558912)接口。 它是打开设备的 framework 表示形式。 当应用程序打开通过 Microsoft Win32 设备[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)函数，框架将创建文件对象来表示打开的设备实例。 因此，框架文件对象是从概念上等效于从应用程序的调用返回的 Win32 句柄**CreateFile**。 框架可创建多个与单个设备相关联的文件对象。 每个文件对象创建每次成功调用**CreateFile**。 所有 I/O 操作，如读取和写入操作，以特定的文件对象实例为都目标。

**请注意**  传递给 UMDF 驱动程序的所有请求都都将与文件对象相关联。 但是，请求传递给[WDM](https://msdn.microsoft.com/library/windows/hardware/ff565698)并[KMDF](https://msdn.microsoft.com/library/windows/hardware/ff544296)驱动程序是有时不与文件对象相关联。

 

UMDF 驱动程序可以调用[ **IWDFIoRequest::GetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff559099)方法来获取与请求关联的文件对象。

当您的驱动程序调用[ **GetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff559099)，framework 递增接口上的引用计数。 您的驱动程序会释放时已完成，但接口指针的引用。 若要执行此操作，可以自动使用智能指针递减引用计数时在对象超出上下文或调用[**发行**](https://msdn.microsoft.com/library/windows/desktop/ms682317)上使用它完成操作后的接口。 有关演示如何使用智能指针的代码示例，请参阅**GetFileObject**。

 

 





