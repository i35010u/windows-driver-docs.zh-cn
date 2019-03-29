---
title: 防止创建和关闭通知对驱动程序造成的不平衡
description: 防止创建和关闭通知对驱动程序造成的不平衡
ms.assetid: e6678226-44d3-4b1d-a296-2017bc9c7c37
keywords:
- 创建文件通知 WDK UMDF
- 清理文件通知 WDK UMDF
- 关闭文件通知 WDK UMDF
- 通知 WDK UMDF
- 通知 WDK UMDF，阻止创建和关闭不平衡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a345defc06a05ec82a82838cfe8a1eb1b0c90f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567892"
---
# <a name="preventing-an-imbalance-of-create-and-close-notifications-to-a-driver"></a>防止创建和关闭通知对驱动程序造成的不平衡


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

上部的 UMDF 驱动程序可以使用[ **IWDFDeviceInitialize::AutoForwardCreateCleanupClose** ](https://msdn.microsoft.com/library/windows/hardware/ff556971)方法可控制框架自动转发创建文件，清理文件并关闭文件向设备堆栈中的下一个较低驱动程序的通知。 但是，由于上部的驱动程序设置，所以**AutoForwardCreateCleanupClose**自动转发仅在设备级别上而不是在每个文件级别，转发必须是相同的设备的所有文件。 框架将确保此转发清理文件和关闭文件通知的行为。 如果上部的驱动程序实现[ **IQueueCallbackCreate::OnCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff556841)回调函数，它必须确保所有的创建文件请求并保持一致，其转发行为是相同清理文件和关闭文件通知转发行为。 如果不这样做可能会导致较低的驱动程序以接收不相等量对的调用其**IQueueCallbackCreate::OnCreateFile**方法并[ **IFileCallbackCleanup::OnCleanupFile**](https://msdn.microsoft.com/library/windows/hardware/ff554905)并[ **IFileCallbackClose::OnCloseFile** ](https://msdn.microsoft.com/library/windows/hardware/ff554910)方法。

若要防止低级驱动程序收到的创建文件并关闭文件通知不相等的量，上部的驱动程序必须确保，在其[ **IQueueCallbackCreate::OnCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff556841)回调函数的：

-   其转发行为是针对设备的所有文件相同的。

-   其转发行为是一致的方式的标志参数设置[ **IWDFDeviceInitialize::AutoForwardCreateCleanupClose**](https://msdn.microsoft.com/library/windows/hardware/ff556971)。 那是：
    -   如果该驱动程序将标志设置为**WdfTrue**，驱动程序必须向设备堆栈下的所有创建文件请求都转发。
    -   如果该驱动程序将标志设置为**WdfFalse**，驱动程序不能转发任何在堆栈的下层的创建文件请求。
    -   如果该驱动程序将标志设置为**WdfUseDefault**和：
        -   如果驱动程序功能驱动程序，它必须不转发堆栈的下层的任何文件创建请求。
        -   如果该驱动程序筛选器驱动程序，它必须转发堆栈的下层的所有文件创建请求。

在其中创建文件请求不能转发该驱动程序的情况下，该驱动程序仍然会生成新的低级驱动程序请求，创建文件通过调用[ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)方法创建新的 WDF 文件。 该驱动程序然后可以完成基于新生成的创建文件请求的结果的原始创建文件请求 (即，从结果中**CreateWdfFile**)。

 

 





