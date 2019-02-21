---
title: 定义和导出新的 Guid
description: 定义和导出新的 Guid
ms.assetid: a7deb283-7cab-4f3c-ad96-f8085222456e
keywords:
- 全局唯一标识符 WDK 内核
- Guid WDK 内核
- 标识符 WDK Guid
- 导出 Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec5a2e76726008bdee18a36bf5a7496e3fbbe5e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519918"
---
# <a name="defining-and-exporting-new-guids"></a>定义和导出新的 Guid





定义新驱动程序将导出到其他系统组件、 驱动程序或应用程序的项的 GUID。 例如，其中一个其设备上定义新的 GUID 的自定义的即插即用事件。 若要定义和导出新的 GUID，必须执行以下操作：

1.  选择 GUID 的符号名称。

    选择用于表示 GUID 的用途的名称。 例如，操作系统使用此类名称作为 GUID\_总线\_类型\_PCI 和 PARPORT\_WMI\_分配\_免费\_计数\_GUID。

2.  为使用 Uuidgen.exe 或 Guidgen.exe 的 GUID 生成一个值。 在安装 Microsoft Windows SDK 时，会自动安装 Uuidgen.exe。 Guidgen.exe 是可从[Microsoft Exchange Server GUID 生成器](https://go.microsoft.com/fwlink/p/?linkid=121586)下载页。

    这些实用程序生成一个唯一的、 已格式化的字符串，表示为 128 位值。 "-S"开关 Uuidgen.exe 输出格式化为 C 结构的 GUID。

3.  在相应的头文件中定义的 GUID。

    使用**定义\_GUID**宏 (在中定义 Guiddef.h) 以将其值与相关联的 GUID 符号名称 （请参阅示例 1）。

    **示例 1:仅限 GUID 的标头文件中定义的 Guid**

    ```cpp
    :
     
    DEFINE_GUID( GUID_BUS_TYPE_PCMCIA, 0x09343630L, 0xaf9f, 0x11d0, 
        0x92,0x9f, 0x00, 0xc0, 0x4f, 0xc3, 0x40, 0xb1 );
    DEFINE_GUID( GUID_BUS_TYPE_PCI, 0xc8ebdfb0L, 0xb510, 0x11d0, 
        0x80,0xE9, 0x00, 0x00, 0xf8, 0x1e, 0x1b, 0x30 );
     
    :
    ```

    如果在包含非 GUID 定义语句的标头文件中定义 GUID，则必须采取额外的步骤来确保 GUID 实例化包含头文件的驱动程序中。 **定义\_GUID**语句必须出现任何外部 **\#ifdef**避免多次包含的语句。 否则，如果标头文件包含在预编译标头，GUID 不是使用标头文件的驱动程序中实例化。 混合标头文件中的示例 GUID 定义，请参阅示例 2。

    **示例 2:在混合的标头文件中定义的 Guid**

    ```cpp
    #ifndef _NTDDSER_    // this ex. is from a serial driver .h file
    #define _NTDDSER_
     
    :
    // Put other header file definitions here.
    :
     
    #endif  // _NTDDSER_
     
    #ifdef DEFINE_GUID   // Do not break compiles of drivers that 
                         // include this header but that do not
                         // want the GUIDs.
    //
    // Put GUID definitions outside of the multiple inclusion 
    // protection.
     
    DEFINE_GUID(GUID_CLASS_COMPORT, 0x86e0d1e0L, 0x8089, 0x11d0, 0x9c,
        0xe4, 0x08, 0x00, 0x3e, 0x30, 0x1f, 0x73);
     
    DEFINE_GUID (GUID_SERENUM_BUS_ENUMERATOR, 0x4D36E978, 0xE325, 
        0x11CE, 0xBF, 0xC1, 0x08, 0x00, 0x2B, 0xE1, 0x03, 0x18);
     
    :
    #endif  // DEFINE_GUID
    ```

    将防止多个包含的语句外部的 GUID 定义不会导致多个实例的 guid 驱动程序由于**定义\_GUID**将 GUID 定义为外部\_C 变量。 允许对外部变量的多个声明，只要的类型匹配。

4.  当创建新的 GUID[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)或[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)，适用以下规则：
    -   不要使用单个 GUID 来标识设备安装程序类和设备接口类。

    -   在创建时与 GUID 关联的符号名称，使用以下约定：

        对于设备安装程序类，使用格式 GUID\_DEVCLASS\_*XXX*。

        对于设备接口的类，使用 GUID 的格式\_DEVINTERFACE\_*XXX*。

 

 




