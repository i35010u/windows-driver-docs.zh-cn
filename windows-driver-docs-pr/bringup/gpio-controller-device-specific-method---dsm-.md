---
title: GPIO 控制器特定于设备的方法 (_DSM)
description: 若要支持各种特定于设备的类的 Windows 中的通用 I/O (GPIO) 驱动程序堆栈和平台固件之间的通信，Microsoft 定义了特定于设备的方法 (_DSM) 可以包含在 ACPI 中的 GPIO 控制器命名空间。
ms.assetid: 2891A78C-8C4F-4FE4-AB69-402F04DFA885
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9223bb68b3869bafa9e3c04a3c41c6781f42534
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534634"
---
# <a name="gpio-controller-device-specific-method-dsm"></a>GPIO 控制器特定于设备的方法 (\_DSM)


若要支持各种特定于设备的类的 Windows 中的通用 I/O (GPIO) 驱动程序堆栈和平台固件之间的通信，Microsoft 定义了特定于设备的方法 (\_DSM)，可以包括在 GPIO 控制器在 ACPI 名称空间。

目前，此方法定义两个函数：

-   **函数索引 0**:标准查询函数的所有\_DSM 方法将要求提供。
-   **函数索引 1**:ActiveBoth 极性函数，它会通知不是在控制器上任何 ActiveBoth 引脚 GPIO 堆栈添加逻辑低。 GPIO 堆栈假定，ActiveBoth pin 添加逻辑低，所以此函数允许重写该默认值为特定球瓶的平台。

## <a name="guid-definition"></a>GUID 定义


GPIO 控制器 GUID \_DSM 方法被定义为：

`{4F248F40-D5E2-499F-834C-27758EA1CD3F}`

## <a name="function-0"></a>函数 0


函数的每个\_DSM 是返回集支持的函数的索引，并始终是必需的查询函数。 有关函数 0 的定义，请参阅部分 9.14.1，"\_DSM （设备特定的方法）"，在[ACPI 5.0 规范](https://www.uefi.org/specifications)。

## <a name="function-1"></a>函数 1


函数的 GPIO 控制器 1 的参数\_DSM 方法定义，如下所示：

### <a name="arguments"></a>参数

-   **Arg0:** GPIO 控制器 UUID \_DSM

    `// GUID: {4F248F40-D5E2-499F-834C-27758EA1CD3F}`

    `DEFINE_GUID (GPIO_CONTROLLER _DSM_GUID,`

    `0x4f248f40, 0xd5e2, 0x499f, 0x83, 0x4c, 0x27, 0x75, 0x8e, 0xa1, 0xcd. 0x3f);`

-   **Arg1:** 修订 ID

    `#define GPIO_CONTROLLER _DSM_REVISION_ID     0`

-   **Arg2:** ActiveBoth 函数索引添加极性：

    `#define GPIO_CONTROLLER_DSM_ACTIVE_BOTH_POLARITY_FUNCTION_INDEX  1`

-   **Arg3:** 包为空 （未使用）

### <a name="return"></a>返回

整数，其中每个是 GPIO 控制器，该域控制器上的 pin 的控制器相对 pin 号码包：

-   定义为 ActiveBoth 中断，并
-   其断言状态*不*逻辑低 (即*是*逻辑高)。

例如，如果一个模拟的 ActiveBoth 插针连接到按钮设备时，pin 将进入*断言*状态 （在 pin 逻辑高输入级别） 当用户按下按钮、 文本框和时用户按住停留在断言状态向下按钮。 当用户释放左键时，pin 状态将变为*unasserted* （输入的逻辑低级别）。

## <a name="asl-code-example"></a>ASL 代码示例


下面的代码示例 ASL 标识一组具有的 ActiveHigh 初始极性的 GPIO 插针。

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

 

 




