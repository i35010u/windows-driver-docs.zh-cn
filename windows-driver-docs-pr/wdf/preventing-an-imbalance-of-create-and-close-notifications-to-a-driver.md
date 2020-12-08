---
title: 防止创建和关闭通知对驱动程序造成的不平衡
description: 防止创建和关闭通知对驱动程序造成的不平衡
keywords:
- 创建文件通知 WDK UMDF
- 清除-文件通知 WDK UMDF
- 关闭文件通知 WDK UMDF
- 通知 WDK UMDF
- 通知 WDK UMDF，阻止创建和关闭不平衡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0792400861e0cfcedc012eef65a53e706a66b71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802125"
---
# <a name="preventing-an-imbalance-of-create-and-close-notifications-to-a-driver"></a>防止创建和关闭通知对驱动程序造成的不平衡


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

高版本的 UMDF 驱动程序可以使用 [**IWDFDeviceInitialize：： AutoForwardCreateCleanupClose**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-autoforwardcreatecleanupclose) 方法控制框架自动将创建文件、清理文件和关闭文件通知转发到设备堆栈中下一个较低的驱动程序的时间。 但是，由于上部驱动程序将 **AutoForwardCreateCleanupClose** 设置为仅在设备级别上自动转发，而不是在每个文件级别上自动转发，因此对于设备的所有文件，转发必须相同。 框架可确保清除文件和关闭文件通知的这种转发行为。 如果上面的驱动程序实现了 [**IQueueCallbackCreate：： OnCreateFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile) 回调函数，则它必须确保其转发行为对于所有创建文件请求都是相同的，并且与清除文件和关闭文件通知的转发行为一致。 如果不这样做，可能会导致较低的驱动程序收到对其 **IQueueCallbackCreate：： OnCreateFile** 方法和 [**IFileCallbackCleanup：： OnCleanupFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile) 和 [**IFileCallbackClose：： OnCloseFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile) 方法的不相等的调用。

若要防止驱动程序收到不等的创建文件和关闭文件通知的数量，则上层驱动程序必须确保在其 [**IQueueCallbackCreate：： OnCreateFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile) 回调函数中执行以下操作：

-   对于设备的所有文件，其转发行为都是相同的。

-   其转发行为与它设置 [**IWDFDeviceInitialize：： AutoForwardCreateCleanupClose**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-autoforwardcreatecleanupclose)的标志参数的方式一致。 即：
    -   如果驱动程序将标志设置为 **WdfTrue**，则驱动程序必须将所有 create file 请求按设备堆栈向下转发。
    -   如果驱动程序将标志设置为 **WdfFalse**，则驱动程序不能将任何创建文件请求沿堆栈向下转发。
    -   如果驱动程序将标志设置为 **WdfUseDefault** ，并：
        -   如果驱动程序是函数驱动程序，则它不能将任何创建文件请求沿堆栈向下移动。
        -   如果驱动程序是筛选器驱动程序，则必须将所有创建文件请求沿堆栈向下转发。

当驱动程序无法转发创建文件请求时，驱动程序仍可以通过调用 [**IWDFDevice：： CreateWdfFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile) 方法来创建新的 WDF 文件，为较低的驱动程序生成新的创建文件请求。 然后，该驱动程序可以基于新生成的创建文件 (请求的结果，根据 **CreateWdfFile**) 的结果来完成原始创建文件请求。

 

