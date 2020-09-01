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
ms.openlocfilehash: 1c76415396d3d103374b075bc9d32228dd758687
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192111"
---
# <a name="framework-file-object"></a>框架文件对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架文件对象通过 [IWDFFile](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile) 接口向驱动程序公开。 它是已打开设备的框架表示形式。 当应用程序通过 Microsoft Win32 [**CreateFile**](/windows/desktop/api/fileapi/nf-fileapi-createfilea) 函数打开设备时，框架会创建一个文件对象来表示打开的设备实例。 因此，框架文件对象在概念上等效于从应用程序调用 **CreateFile**返回的 Win32 句柄。 框架可创建多个与单个设备关联的文件对象。 每次成功调用 **CreateFile**时都会创建每个文件对象。 所有 i/o 操作（如读取和写入）以特定的文件对象实例为目标。

**注意**   传递给 UMDF 驱动程序的所有请求都与文件对象相关联。 但是，传递到 [WDM](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) 和 [KMDF](./index.md) 驱动程序的请求有时不与文件对象相关联。

 

UMDF 驱动程序可以调用 [**IWDFIoRequest：： GetFileObject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject) 方法来获取与请求关联的文件对象。

当驱动程序调用 [**GetFileObject**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject)时，框架会递增接口上的引用计数。 当你的驱动程序结束时，你的驱动程序将负责释放该引用。 若要执行此操作，请使用智能指针，该指针会在对象离开上下文时自动递减引用计数，或在完成后调用接口上的 [**发布**](/windows/desktop/api/unknwn/nf-unknwn-iunknown-release) 。 有关演示如何使用智能指针的代码示例，请参阅 **GetFileObject**。

 

