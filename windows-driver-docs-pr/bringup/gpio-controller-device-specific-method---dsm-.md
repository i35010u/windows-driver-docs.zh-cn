---
title: GPIO 控制器的特定于设备的方法 (_DSM)
description: 为了支持 Windows 和平台固件中的常规用途 i/o (GPIO) 驱动程序堆栈之间的各种特定于设备的通信，Microsoft 定义了可在 ACPI 命名空间中的 GPIO 控制器下包含的 Device-Specific 方法 (_DSM) 。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9dfcfc19c856e6a5ae6239bc8c7847b43f3904
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788995"
---
# <a name="gpio-controller-device-specific-method-_dsm"></a>GPIO 控制器 Device-Specific 方法 (\_ DSM) 


为了支持 Windows 和平台固件中的常规用途 i/o (GPIO) 驱动程序堆栈之间的各种特定于设备的通信，Microsoft 定义了 \_ 可在 ACPI 命名空间中的 GPIO 控制器下包含的 Device-Specific 方法 (DSM) 。

目前，此方法定义了两个函数：

-   **函数索引 0**：所有 \_ DSM 方法都需要提供的标准查询函数。
-   **函数索引 1**： ActiveBoth 极性函数，该函数通知控制器上不断言逻辑低的任何 ActiveBoth PIN 的 GPIO 堆栈。 GPIO 堆栈假设 ActiveBoth 的 pin 断言逻辑较低，因此此函数允许平台替代特定 pin 的默认值。

## <a name="guid-definition"></a>GUID 定义


GPIO 控制器 DSM 方法的 GUID \_ 定义为：

`{4F248F40-D5E2-499F-834C-27758EA1CD3F}`

## <a name="function-0"></a>函数0


每个 DSM 的函数 0 \_ 是一个查询函数，它返回支持的函数索引集，并且始终是必需的。 有关函数0的定义，请参阅 \_ [ACPI 5.0 规范](https://uefi.org/specifications)中的 9.14.1 "DSM (设备特定的方法) " 部分。

## <a name="function-1"></a>函数1


GPIO 控制器 DSM 方法的函数1的参数 \_ 定义如下：

### <a name="arguments"></a>自变量

-   **Arg0：** GPIO 控制器 DSM 的 UUID \_

    `// GUID: {4F248F40-D5E2-499F-834C-27758EA1CD3F}`

    `DEFINE_GUID (GPIO_CONTROLLER _DSM_GUID,`

    `0x4f248f40, 0xd5e2, 0x499f, 0x83, 0x4c, 0x27, 0x75, 0x8e, 0xa1, 0xcd. 0x3f);`

-   **Arg1：** 修订 ID

    `#define GPIO_CONTROLLER _DSM_REVISION_ID     0`

-   **Arg2：** ActiveBoth 断言极性的函数索引：

    `#define GPIO_CONTROLLER_DSM_ACTIVE_BOTH_POLARITY_FUNCTION_INDEX  1`

-   **Arg3：** 包空 (未使用) 

### <a name="return"></a>返回

一个整数包，其中每个整数都是 GPIO 控制器上的 pin 的控制器相对 pin 号，即：

-   定义为 ActiveBoth 中断，
-   断言状态 *不* 是逻辑低 (换言之， *是* 逻辑高) 。

例如，如果某个模拟的 ActiveBoth pin 连接到一个按钮设备，则当用户按下该按钮时，该 pin 将进入 "已 *断言* " 状态 (逻辑高的输入级别，) ，当用户按下该按钮时保持已断言状态。 当用户释放按钮时，pin 状态将更改为 " *unasserted* (逻辑-低输入级别) 。

## <a name="asl-code-example"></a>ASL 代码示例


以下 ASL 代码示例标识了一组具有 ActiveHigh 初始极性的 GPIO pin。

```asl
//
// _DSM - Device-Specific Method
//
// Arg0:    UUID       Unique function identifier
// Arg1:    Integer    Revision Level
// Arg2:    Integer    Function Index (0 = Return Supported Functions)
// Arg3:    Package    Parameters
//

Function(_DSM,{BuffObj, PkgObj, IntObj},{BuffObj, IntObj, IntObj, PkgObj})
{

    //
    // Switch based on which unique function identifier was passed in
    //

    //
    // GPIO CLX UUID
    //

    If(LEqual(Arg0,ToUUID("4F248F40-D5E2-499F-834C-27758EA1CD3F")))
    {
        switch(Arg2)
        {

            //
            // Function 0: Return supported functions, based on 
            //    revision
            //

            case(0)
            {
                // Revision 0+: Functions 0 & 1 are supported
                return (Buffer() {0x3})
            }

            //
            // Function 1: For emulated ActiveBoth controllers, 
            //    returns a package of controller-relative pin
            //    numbers. Each corresponding pin will have an
            //    initial polarity of ActiveHigh.
            //
            //    A pin number of 0xffff is ignored.
            //

            case(1)
            {     
                // Marks pins 0x28, 0x29 and 0x44 to be ActiveHigh.
                Return (Package() {0x28, 0x29, 0x44})
            }

            //
            // Unrecognized function for this revision
            //

            default
            {
                BreakPoint
            }
        }
    }
    else
    {
        //
        // If this is not one of the UUIDs we recognize, then return
        // a buffer with bit 0 set to 0 to indicate that no functions
        // are supported for this UUID.
        //

        return (Buffer() {0})
    }
}
```

 

 




