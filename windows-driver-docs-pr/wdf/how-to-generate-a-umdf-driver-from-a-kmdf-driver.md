---
title: 如何将 KMDF 驱动程序转换为 UMDF 2 驱动程序（反之亦然）
description: 本主题介绍如何将内核模式驱动程序框架（KMDF）驱动程序转换为用户模式驱动程序框架（UMDF）版本2驱动程序，反之亦然。
ms.assetid: 69B865CF-65D0-4211-951B-6574E27F10BD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 997c47d97ad3489af5ceff825300a6debcc67289
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845218"
---
# <a name="how-to-convert-a-kmdf-driver-to-a-umdf-2-driver-and-vice-versa"></a>如何将 KMDF 驱动程序转换为 UMDF 2 驱动程序（反之亦然）


本主题介绍如何将内核模式驱动程序框架（KMDF）驱动程序转换为用户模式驱动程序框架（UMDF）版本2驱动程序，反之亦然。

## <a name="driver-conversion-using-visual-studio"></a>使用 Visual Studio 的驱动程序转换


1.  从 KMDF 切换到 UMDF 时，请使用**用户模式驱动程序、空（UMDF V2）** 项目模板在 Visual Studio 中创建一个空的 UMDF 项目。 从 UMDF 切换到 KMDF 时，请使用**内核模式驱动程序、空（KMDF）** 项目模板在 Visual Studio 中创建一个空的 KMDF 项目。

    Visual Studio 将使用适当的设置创建一个空的驱动程序项目，并创建一个针对指定框架的 INF 文件。

2.  将源代码和标头文件从以前的驱动程序复制到新项目中。
3.  更新标头文件。 对于 UMDF，请包含 Windows .h。 对于 KMDF，请包含 Ntddk。 Wdf 是 KMDF 和 UMDF 所共有的，因此请将其包含在这两种类型的驱动程序中。

    （可选）使用 **\_内核\_模式**预处理器宏，按条件添加适当的系统标头：

    ```cpp
    #ifndef _KERNEL_MODE
    // This is a user-mode driver
    #include <windows.h>

    #else
    // This is a kernel-mode driver
    #include <ntddk.h>
    #define NTSTRSAFE_LIB
    #include <ntstrsafe.h>
    #endif

    // This is a common WDF header (for both KMDF and UMDF)
    #include <wdf.h> 
    ```

4.  将源代码更新为删除或有条件地编译（使用 **\_内核\_模式**宏）目标驱动程序模型中不支持的任何功能。 例如：

    -   如果你的驱动程序使用 WPP 跟踪，请[\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏来更新 WPP。 此宏在用户模式和内核模式下采用不同的参数。
        ```cpp
        WPP_INIT_TRACING ( DriverObject, RegistryPath ); // KMDF
        WPP_INIT_TRACING ( “<MyDriverNameString>” ); // UMDF
        ```

    -   如果要转换的 KMDF 驱动程序调用了 WDM 例程（如[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)），请将其替换为相应的 WDF 方法，例如[**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)。 同样，如果要转换调用用户模式功能的 UMDF 驱动程序，请将其替换为等效的内核模式例程。
    -   某些方法仅在 KMDF 中受支持，而其他方法仅在 UMDF 中受支持。 有关所有 Windows 驱动程序框架（WDF）方法及其框架适用性的列表，请参阅[WDF 回调和方法摘要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)。

 

 





