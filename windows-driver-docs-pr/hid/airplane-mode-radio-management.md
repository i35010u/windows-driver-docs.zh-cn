---
title: 飞行模式无线管理
description: 从 Windows 8 开始，Windows 操作系统将通过 HID 为飞行模式无线电管理控制提供支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df4d660d91511643b3a294a8351cdd8f78f272f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791559"
---
# <a name="airplane-mode-radio-management"></a>飞行模式无线管理


从 Windows 8 开始，Windows 操作系统将通过 HID 为飞行模式无线电管理控制提供支持。

## <a name="architecture-and-overview"></a>体系结构和概述


飞行模式的目标是让 PC 制造商提供按钮或交换机 (，并可能指示状态) 使最终用户能够在一次中启用/关闭所有无线控制。 这主要使需要打开/关闭飞行模式的用户能够以编程方式执行此操作，以允许操作系统 () 标识交换机的状态， (b) 通过软件控制各种无线无线电收发器。

Windows 在 "一般桌面使用情况" 页上提供对以下 HID 用法的支持。

| 使用 ID | 使用名称                   | 使用情况类型                 |
|----------|------------------------------|----------------------------|
| 0x000C   | 无线广播 Controlls     | CollectionApplication (CA)  |
| 0x00C6   | 无线单选按钮        | 开启/关闭控件 (OOC)        |
| 0x00C7   | 无线无线电 LED           | 开启/关闭控件 (OOC)        |
| 0x00C8   | 无线收音机滑块开关 | 开启/关闭控件 (OOC)        |

 

下面是为无线电管理/飞行模式提供支持的 HID 客户端的体系结构关系图。

![飞行模式体系结构](images/airplane-mode.png)

ShellHW 检测服务 ( # A0) 是在用户模式下运行并为无线电管理设备提供支持的 HID 客户端驱动程序/服务。 监视是否存在类型为的 HID 顶级集合

-   使用情况 \_ 页 (通用桌面) 05 01
-   使用情况 (无线无线电控制) 09 0C

## <a name="sample-report-descriptor"></a>示例报表描述符


以下部分提供了 PC 制造商必须利用的示例报表描述符。 请注意，如果顶层集合是已有另一个顶级集合的报表描述符的一部分，则必须包含报表 ID (不会在下面的示例) 中显示。

下一节提供了有关 PC 制造商的其他信息，并确定哪个报表描述符示例最适合其系统设计：

-   "无状态" 按钮通常在键盘使用者控件按钮上使用， (独立或与许多移动系统上的 "函数" 按钮一起使用 (例如 Fn + F5) # A3。
-   滑块开关通常用于在移动系统上打开/关闭开关 (例如，使用 "在飞机上打开/关闭交换机) 的便携式计算机"。
-   LED 通常用作独立飞机的更多指示器，或与无状态按钮或滑块开关结合使用。 Windows 用户无需在移动外观系统上使用此 LED，因为用户界面周围的视觉对象指示与飞行模式有关。

*无 LED 的无状态按钮*

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

*带有 LED 的无状态按钮*

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

*不带 LED) 的滑块开关 (*

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

*带有 LED 的滑块开关*

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

*LED 仅 (没有按钮或滑块)*

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


提示 \# 1：使用收音机管理器按钮时，PC 制造商应在按钮被释放时发送一个 HID 报表，而不是在按下按钮时发送。 这是因为切换按钮通常是相对输入而不是绝对的。

提示 \# 2：飞行模式无线电管理 HID 使用情况仅在移动系统上运行 (备有电池的) 并且需要 windows 8 或更高版本的 windows。

提示 \# 3：有关 "飞行模式" "无线电管理" 按钮的详细信息，请参阅 [Windows 8 白皮书的键盘增强功能](/previous-versions/windows/hardware/design/dn613956(v=vs.85)) 。

提示 \# 4：有关按钮的详细信息，若要确保实施正确的硬件，请查看 Windows 8 系统徽标要求。

 

