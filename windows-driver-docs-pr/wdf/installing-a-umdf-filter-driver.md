---
title: 安装 UMDF 筛选器驱动程序
description: 筛选器驱动程序可以支持特定设备或安装程序类中的所有设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0e30a0322305d8d1e44267665e536095ee6a639
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837605"
---
# <a name="installing-a-umdf-filter-driver"></a>安装 UMDF 筛选器驱动程序


筛选器驱动程序可以支持特定设备或安装程序类中的所有设备。 较低版本的筛选器驱动程序会附加到设备的功能驱动程序以下，而上层筛选器会附加到设备的功能驱动程序之上。

本主题介绍如何安装和配置 User-Mode Driver Framework (UMDF) 特定于设备的 (上或下) 筛选器驱动程序。 不能使用 UMDF 来编写类筛选器驱动程序。 本主题适用于 UMDF 版本1和2。

构建设备堆栈的结构时，请记住，框架目前仅支持每个堆栈一个连续的 UMDF 驱动程序块。 此外，不能在同一设备堆栈中安装 UMDF 版本1和版本2驱动程序。

**如何安装和配置驱动程序**

1.  UMDF 1 筛选器驱动程序应从其 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数调用 [**IWDFDeviceInitialize：： SetFilter**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter) 。 从 UMDF 版本2开始，驱动程序将调用 [**WdfFdoInitSetFilter**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetfilter)。

2.  除了驱动程序可以指定的任何特定于 UMDF 的指令外，还必须指定 **UmdfService** 和 **UmdfServiceOrder** 指令。 在本主题中，我们将指定上方筛选器驱动程序：

    ```cpp
    [<mydriver>_Install.NT.Wdf]
    UmdfService=UMDFFunction,WUDFFuncDriver_Install
    UmdfService=UMDFFilter,UMDFFilter_Install
    UmdfServiceOrder=UMDFFunction,UMDFFilter
    ```

    驱动程序将按照它们在 **UmdfServiceOrder** 项中的列出顺序添加到设备堆栈中。 第一个参数指定设备堆栈中最低的 UMDF 驱动程序。 若要安装更低的筛选器驱动程序，只需反转 **UmdfServiceOrder** 的参数。

    有关这些和其他 UMDF 特定 INF 指令的详细信息，请参阅 [在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

3.  如果驱动程序的设备堆栈只包含 UMDF 驱动程序，请跳过此步骤。

    如果驱动程序的设备堆栈包含任何不是 UMDF 的驱动程序，则 INF 文件必须包含将反射器指定为上层筛选器驱动程序的 **AddReg** 部分：

    ```cpp
    [<mydriver>_Device_AddReg]
    ; Load the redirector as an upperfilter on this specific device.
    ; 0x00010008 - FLG_ADDREG_TYPE_MULTI_SZ | FLG_ADDREG_APPEND
    HKR,,"UpperFilters",0x00010008,"WUDFRd" 
    ```

4.  将驱动程序作为上限筛选器加载后，它负责将 i/o 请求转发到堆栈中的下一个驱动程序。 为了说明这一点，请考虑一个简单的直通驱动程序， (UMDF 版本 1) 高于 KMDF 函数驱动程序。

    首先，检索默认 i/o 目标的接口 (堆栈) 中的下一个驱动程序。 然后，格式化并发送请求。 最简单的方案如下所示：

    ```cpp
    IWDFIoTarget * kmdfIoTarget = NULL;
        
        this->GetFxDevice()->GetDefaultIoTarget (&kmdfIoTarget);

        Request->FormatUsingCurrentType();

        hr = Request->Send (
            kmdfIoTarget, 
            0,  // 0 Submits Asynchronous else use WDF_REQUEST_SEND_OPTION_SYNCHRONOUS
            0);
    ```

 

