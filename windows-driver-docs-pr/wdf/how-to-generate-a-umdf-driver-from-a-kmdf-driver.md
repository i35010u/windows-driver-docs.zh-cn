---
title: 如何将 KMDF 驱动程序转换为 UMDF 2 驱动程序 （和进行相反转换）
description: 本主题介绍如何将内核模式驱动程序框架 (KMDF) 驱动程序转换成用户模式驱动程序框架 (UMDF) 版本 2 驱动程序和进行相反转换。
ms.assetid: 69B865CF-65D0-4211-951B-6574E27F10BD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69cbfe374c5bc881741a320f52e74cfea00ed2fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533541"
---
# <a name="how-to-convert-a-kmdf-driver-to-a-umdf-2-driver-and-vice-versa"></a>如何将 KMDF 驱动程序转换为 UMDF 2 驱动程序 （和进行相反转换）


本主题介绍如何将内核模式驱动程序框架 (KMDF) 驱动程序转换成用户模式驱动程序框架 (UMDF) 版本 2 驱动程序和进行相反转换。

## <a name="driver-conversion-using-visual-studio"></a>使用 Visual Studio 的驱动程序转换


1.  当从 KMDF 切换到 UMDF，Visual Studio 中使用创建空 UMDF 项目**用户模式驱动程序，为空 (UMDF V2)** 项目模板。 当从 UMDF 切换到 KMDF，Visual Studio 中使用创建空 KMDF 项目**内核模式驱动程序、 为空 (KMDF)** 项目模板。

    Visual Studio 将使用相应的设置，以及针对指定框架的 INF 文件创建一个空的驱动程序项目。

2.  将从以前的驱动程序的源代码和标头文件复制到新的项目。
3.  更新标头文件。 对于 UMDF，包括 Windows.h。 对于 KMDF，包括 Ntddk.h。 Wdf.h 是普遍适用于 KMDF 和 UMDF，因此将其包含在这两种类型的驱动程序。

    （可选） 使用 **\_内核\_模式** 预处理器宏有条件地添加正确的系统标头：

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

4.  更新要删除或有条件地编译的源代码 (使用 **\_内核\_模式** 宏) 中的目标驱动程序模型不支持任何功能。 例如：

    -   如果您的驱动程序使用 WPP 跟踪，请更新[WPP\_INIT\_跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556191)宏。 此宏将在用户模式和内核模式下的不同参数。
        ```cpp
        WPP_INIT_TRACING ( DriverObject, RegistryPath ); // KMDF
        WPP_INIT_TRACING ( “<MyDriverNameString>” ); // UMDF
        ```

    -   如果要转换的 KMDF 驱动程序，如调用 WDM 例程[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)，替换它们与相应的 WDF 方法，如[ **WdfMemoryCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548706)。 同样，如果要将转换调用用户模式下函数 UMDF 驱动程序，将其替换为等效的内核模式例程。
    -   当仅在 UMDF 中支持的其他人时仅在 KMDF，支持某些方法。 Windows 驱动程序框架 (WDF) 的所有方法和 framework 适用性的列表，请参阅[WDF 回调摘要和方法](https://msdn.microsoft.com/library/windows/hardware/dn265591)。

 

 





