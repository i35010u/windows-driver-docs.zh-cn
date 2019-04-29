---
title: 安装 UMDF 筛选器驱动程序
description: 筛选器驱动程序可以支持特定设备或所有设备安装程序类中。
ms.assetid: AE6D4E36-B758-451A-983E-6F0D7ADFD7A7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009e718c2a1b1f2b0f58358960f0f4f926eb0c95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378067"
---
# <a name="installing-a-umdf-filter-driver"></a>安装 UMDF 筛选器驱动程序


筛选器驱动程序可以支持特定设备或所有设备安装程序类中。 上部的筛选器将附加设备的功能驱动程序之上时，较低的筛选器驱动程序将附加设备的功能驱动程序，如下。

本主题介绍如何安装和配置用户模式驱动程序框架 (UMDF) 特定于设备的 （上限或下限） 筛选器驱动程序。 您不能使用 UMDF 编写类筛选器驱动程序。 本主题适用于这两种 UMDF 版本 1 和 2。

结构设备堆栈，请记住框架当前支持的每个堆栈的 UMDF 驱动程序只能有一个连续的块。 此外，不能在同一个设备堆栈中安装 UMDF 版本 1 和版本 2 的驱动程序。

**如何安装和配置您的驱动程序**

1.  UMDF 1 筛选器驱动程序应调用[ **IWDFDeviceInitialize::SetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff556985)从其[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)回调函数。 从 UMDF 版本 2 开始，您的驱动程序改为调用[ **WdfFdoInitSetFilter**](https://msdn.microsoft.com/library/windows/hardware/ff547273)。

2.  除了您的驱动程序可以指定任何特定于 UMDF 的指令，还必须指定**UmdfService**并**UmdfServiceOrder**指令。 在本主题中，我们将指定的上限的筛选器驱动程序：

    ```cpp
    [<mydriver>_Install.NT.Wdf]
    UmdfService=UMDFFunction,WUDFFuncDriver_Install
    UmdfService=UMDFFilter,UMDFFilter_Install
    UmdfServiceOrder=UMDFFunction,UMDFFilter
    ```

    驱动程序添加到设备堆栈中列出的顺序**UmdfServiceOrder**条目。 第一个参数指定最低 UMDF 驱动程序设备堆栈中。 若要安装较低的筛选器驱动程序，只需反转的参数**UmdfServiceOrder**。

    有关这些和其他特定于 UMDF 的 INF 指令的详细信息，请参阅[INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

3.  如果您的驱动程序设备堆栈包含 UMDF 驱动程序，请跳过此步骤。

    如果您的驱动程序设备堆栈包含任何不所 UMDF 驱动程序，您的 INF 文件必须包括**AddReg**作为上限的筛选器驱动程序指定该发送程序的部分：

    ```cpp
    [<mydriver>_Device_AddReg]
    ; Load the redirector as an upperfilter on this specific device.
    ; 0x00010008 - FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
    HKR,,"UpperFilters",0x00010008,"WUDFRd" 
    ```

4.  您的驱动程序加载为上限的筛选器后，它负责转发对堆栈中的下一步驱动程序的 I/O 请求。 若要说明，请考虑的简单直通驱动程序 (UMDF 第 1 版) 高于 KMDF 功能驱动程序。

    首先，检索默认 I/O 目标的接口 （在堆栈中的下一步驱动程序）。 然后，设置格式并将请求发送。 最简单的方案如下所示：

    ```cpp
    IWDFIoTarget * kmdfIoTarget = NULL;
        
        this->GetFxDevice()->GetDefaultIoTarget (&kmdfIoTarget);

        Request->FormatUsingCurrentType();

        hr = Request->Send (
            kmdfIoTarget, 
            0,  // 0 Submits Asynchronous else use WDF_REQUEST_SEND_OPTION_SYNCHRONOUS
            0);
    ```

 

 





