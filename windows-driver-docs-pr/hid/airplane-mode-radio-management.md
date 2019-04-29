---
title: 飞行模式无线管理
description: 从 Windows 8 开始，Windows 操作系统提供了通过 HID，对飞行模式单选管理控件的支持。
ms.assetid: 5B0662B0-CBD3-4F31-B98F-6BC8184574DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c55bdac9dd253b236aa95afe77b07d5cfbc08b18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390418"
---
# <a name="airplane-mode-radio-management"></a>飞行模式无线管理


从 Windows 8 开始，Windows 操作系统提供了通过 HID，对飞行模式单选管理控件的支持。

## <a name="architecture-and-overview"></a>体系结构和概述


飞行模式的目的是允许 PC 制造商联系，以提供一个按钮或交换机 （和可能的 LED 来指示状态），使最终用户可以启用/禁用在一个操作中的所有无线控件。 这主要是使用户需要打开 / 关闭飞行模式，可以为此，请在各种无线通过软件无线电收发器的编程方法允许操作系统 （a） 识别的开关和 (b) 控制的状态。

Windows 提供了普通台式计算机使用情况页面上的以下 HID 用法的支持。

| 使用 ID | 用法的名称                   | 使用类型                 |
|----------|------------------------------|----------------------------|
| 0x000C   | 无线电 Controlls     | CollectionApplication (CA) |
| 0x00C6   | 无线单选按钮        | 打开/关闭控件 (OOC)       |
| 0x00C7   | 无线电 LED           | 打开/关闭控件 (OOC)       |
| 0x00C8   | 无线功能滑块开关 | 打开/关闭控件 (OOC)       |

 

以下是为单选管理提供支持的隐藏客户端的体系结构图 / 飞行模式。

![飞行模式体系结构](images/airplane-mode.png)

ShellHW 检测服务 (SHSVCD.dll) 是隐藏客户端驱动程序/服务，在用户模式下运行并为单选管理设备提供支持。 它会监视存在的 HID 顶部级别类型的集合

-   使用情况\_页 （普通台式计算机） 05 01
-   使用情况 （无线电控件） 09 0 C

## <a name="sample-report-descriptor"></a>示例报告描述符


以下部分提供了 PC 制造商必须利用的示例报告描述符。 请注意，是否顶部级别集合是已具有另一个顶部级别集合的报告描述符的一部分，报表 ID 必须包含 （在下面的示例中未显示）。

下一节提供有关 PC 制造商的其他信息，并标识哪个报表描述符示例是最适合他们的系统设计：

-   在键盘消费者控制按钮通常使用无状态的按钮 (无论它们是单机或与许多移动系统 (例如 Fn + F5) 上的函数按钮结合使用)。
-   具有开/关开关 （例如与在飞行模式打开/关闭开关的便携式计算机） 的物理滑块移动系统上通常使用滑块开关。
-   LED 通常是多个指示器用作独立飞机或与任一无状态按钮或滑块开关结合使用。 窗口用户无需使用此移动窗体身份系统上的 LED，如围绕飞行模式在 UI 中的可视指示。

*无状态的按钮，而无需 LED*

``` syntax
USAGE_PAGE (Generic Desktop)                   05 01 
USAGE (Wireless Radio Controls)                09 0C 
COLLECTION (Application)                       A1 01 
LOGICAL_MINIMUM (0)                            15 00 
LOGICAL_MAXIMUM (1)                            25 01 
USAGE (Wireless Radio Button)                  09 C6 
REPORT_COUNT (1)                               95 01 
REPORT_SIZE (1)                                75 01 
INPUT (Data,Var,Rel)                           81 06 
REPORT_SIZE (7)                                75 07 
INPUT (Cnst,Var,Abs)                           81 03 
END_COLLECTION                                 C0
```

*使用 LED 无状态的按钮*

``` syntax
USAGE_PAGE (Generic Desktop)                    05 01 
USAGE (Wireless Radio Controls)                 09 0C 
COLLECTION (Application)                        A1 01 
LOGICAL_MINIMUM (0)                             15 00 
LOGICAL_MAXIMUM (1)                             25 01 
USAGE (Wireless Radio Button)                   09 C6 
REPORT_COUNT (1)                                95 01 
REPORT_SIZE (1)                                 75 01 
INPUT (Data,Var,Rel)                            81 06 
REPORT_SIZE (7)                                 75 07 
INPUT (Cnst,Var,Abs)                            81 03 
USAGE (Wireless Radio LED)                      09 C7 
REPORT_SIZE (1)                                 75 01 
OUTPUT (Data,Var,Rel)                           91 02 
REPORT_SIZE (7)                                 75 07 
OUTPUT (Cnst,Var,Abs)                           91 03 
END_COLLECTION                                  C0
```

*滑块开关 （不带 LED)*

``` syntax
USAGE_PAGE (Generic Desktop)                    05 01 
USAGE (Wireless Radio Controls)                 09 0C 
COLLECTION (Application)                        A1 01 
LOGICAL_MINIMUM (0)                             15 00 
LOGICAL_MAXIMUM (1)                             25 01 
USAGE (Wireless Radio Slider Switch)            09 C8 
REPORT_COUNT (1)                                95 01 
REPORT_SIZE (1)                                 75 01 
INPUT (Data,Var,Abs)                            81 02 
REPORT_SIZE (7)                                 75 07 
INPUT (Cnst,Var,Abs)                            81 03 
END_COLLECTION                                  C0
```

*使用 LED 滑块开关*

``` syntax
USAGE_PAGE (Generic Desktop)                    05 01 
USAGE (Wireless Radio Controls)                 09 0C 
COLLECTION (Application)                        A1 01 
LOGICAL_MINIMUM (0)                             15 00 
LOGICAL_MAXIMUM (1)                             25 01 
USAGE (Wireless Radio Slider Switch)            09 C8 
REPORT_COUNT (1)                                95 01 
REPORT_SIZE (1)                                 75 01 
INPUT (Data,Var,Abs)                            81 02 
REPORT_SIZE (7)                                 75 07 
INPUT (Cnst,Var,Abs)                            81 03 
USAGE (Wireless Radio LED)                      09 C7 
REPORT_SIZE (1)                                 75 01 
OUTPUT (Data,Var,Rel)                           91 02 
REPORT_SIZE (7)                                 75 07 
OUTPUT (Cnst,Var,Abs)                           91 03 
END_COLLECTION                                  C0
```

*LED 仅 （任何按钮或滑块）*

``` syntax
USAGE_PAGE (Generic Desktop)                   05 01 
USAGE (Wireless Radio Controls)                09 0C 
COLLECTION (Application)                       A1 01 
LOGICAL_MINIMUM (0)                            15 00 
LOGICAL_MAXIMUM (1)                            25 01 
USAGE (Wireless Radio LED)                     09 C7 
REPORT_COUNT (1)                               95 01 
REPORT_SIZE (1)                                75 01 
OUTPUT (Data,Var,Rel)                          91 02 
REPORT_SIZE (7)                                75 07 
OUTPUT (Cnst,Var,Abs)                          91 03 
END_COLLECTION                                 C0
```

## <a name="troubleshooting-common-errors"></a>排查常见错误


提示\#1:使用单选 manager 按钮时，PC 制造商应释放按钮时并不是在按下按钮时发送一个 HID 报表。 这是因为切换按钮通常是相对的输入，不是绝对的另一个。

提示\#2:飞行模式无线管理 HID 用法仅在移动系统 （由电池供电） 上运行，需要 Windows 8 或更高版本的 Windows。

提示\#3:有关飞行模式无线管理按钮的详细信息，请参阅[到 Windows 8 的键盘增强功能](https://msdn.microsoft.com/library/windows/hardware/dn613956.aspx)白皮书。

提示\#4:有关详细信息按钮，并以确保实现正确的硬件，请查看 Windows 8 系统徽标要求。

 

 




