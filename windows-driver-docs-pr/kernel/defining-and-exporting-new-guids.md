---
title: 定义和导出新 GUID
description: 定义和导出新 GUID
keywords:
- 全局唯一标识符 WDK 内核
- Guid WDK 内核
- 标识符 WDK Guid
- 导出 Guid
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab307b0c9b3b96398933a4ce2a76a0301625aaba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792799"
---
# <a name="defining-and-exporting-new-guids"></a>定义和导出新 GUID





为驱动程序导出到其他系统组件、驱动程序或应用程序的项目定义新的 GUID。 例如，在其某个设备上为自定义 PnP 事件定义新的 GUID。 若要定义和导出新的 GUID，必须执行以下操作：

1.  选择 GUID 的符号名称。

    选择表示 GUID 用途的名称。 例如，操作系统使用 GUID \_ 总线 \_ 类型为 \_ PCI 和 PARPORT 的 \_ \_ \_ \_ 名称作为 guid \_ 。

2.  使用 Uuidgen.exe 或 Guidgen.exe 生成 GUID 的值。 安装 Microsoft Windows SDK 时，将自动安装 Uuidgen.exe。 可以从 [Microsoft Exchange SERVER GUID 生成器](https://go.microsoft.com/fwlink/p/?linkid=121586) 下载页获取 Guidgen.exe。

    这些实用工具生成一个唯一的格式化字符串，该字符串表示128位值。 Uuidgen.exe 上的 "-s" 开关输出格式为 C 结构的 GUID。

3.  在适当的标头文件中定义 GUID。

    使用在 Guiddef 中定义的 " **定义 \_ guid** 宏" () 将 GUID 符号名称与它的值相关联 (参见 Example 1) 。

    **示例1：在 GUID-Only 头文件中定义 Guid**

    ```cpp
    :
     
    DEFINE_GUID( GUID_BUS_TYPE_PCMCIA, 0x09343630L, 0xaf9f, 0x11d0, 
        0x92,0x9f, 0x00, 0xc0, 0x4f, 0xc3, 0x40, 0xb1 );
    DEFINE_GUID( GUID_BUS_TYPE_PCI, 0xc8ebdfb0L, 0xb510, 0x11d0, 
        0x80,0xE9, 0x00, 0x00, 0xf8, 0x1e, 0x1b, 0x30 );
     
    :
    ```

    如果 GUID 是在包含 GUID 定义以外的语句的标头文件中定义的，则必须采取额外的步骤来确保 GUID 在包含头文件的驱动程序中实例化。 **DEFINE \_ GUID** 语句必须出现在防止多次包含的任何 **\# ifdef** 语句的外部。 否则，如果标头文件包含在预编译标头中，则不会在使用标头文件的驱动程序中实例化该 GUID。 有关混合标头文件中的 GUID 定义示例，请参见示例2。

    **示例2：在混合头文件中定义 Guid**

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

    将 guid 定义置于防止多次包含的语句外不会导致驱动程序中 GUID 的多个实例，因为 **定义 \_ GUID** 将 GUID 定义为 EXTERN \_ C 变量。 只要类型匹配，就允许使用外部变量的多个声明。

4.  为新的 [设备安装程序类](../install/overview-of-device-setup-classes.md) 或 [设备接口类](../install/overview-of-device-interface-classes.md)创建 GUID 时，下列规则适用：
    -   不要使用单个 GUID 来标识设备安装程序类和设备接口类。

    -   创建要与 GUID 关联的符号名称时，请使用以下约定：

        对于设备安装程序类，请使用格式 GUID \_ DEVCLASS \_ *XXX*。

        对于设备接口类，请使用格式 GUID \_ DEVINTERFACE \_ *XXX*。

 

