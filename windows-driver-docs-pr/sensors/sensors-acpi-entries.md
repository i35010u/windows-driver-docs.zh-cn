---
title: 传感器 ACPI 条目
description: 本主题介绍 Windows 10 中特定于传感器的高级配置和电源管理界面 (ACPI) 条目。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63bd572715f43638670e30ca9d702d8eaaf4b022
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805101"
---
# <a name="sensors-acpi-entries"></a>传感器 ACPI 条目


本主题介绍了 Windows 10 移动版中特定于传感器的高级配置和电源管理界面 (ACPI) 条目。 这些条目将添加到 ACPI 源语言 (ASL) 文件中。

## <a name="rotm"></a>ROTM


旋转矩阵 (ROTM) 是一个矩阵，用于描述传感器的 X、Y 和 Z 轴与 (OEM) 定义的移动设备的 X、Y 和 Z 轴之间的关系。

每一行分别表示应用于 X、Y 和 Z 轴的转换。 每个条目是一个介于-1 和1之间的十进制数字，其中每个数字最多有3个小数位数。

例如，在以下 **方法** 中，矩阵指示传感器硬件的 X、Y 和 z 轴分别沿移动设备的 Y、-X 和 z 轴显示。

```cpp
Method(ROTM, 0x0, NotSerialized) {
                Name(RBUF, Package(){
                    "0 1 0",
                    "-1 0 0",
                    "0 0 -1"
                })
                Return (RBUF)
            }
```

## <a name="prim"></a>PRIM


以下 **方法** 将传感器标记为主传感器。

```cpp
Method(PRIM, 0x0, NotSerialized) {
                Name(RBUF, Buffer(){1})
                    Return (RBUF)
            }
```

>[!NOTE]
> 如果移动设备上有多个相同类型的传感器 (例如，多个加速感应器) ，则必须使用 **PRIM** 关键字将其中一个标记为 "主要"。 调用传感器的 Adaptivesourcemanager.getdefault 方法时，WinRT API 将使用主传感器。 主传感器还将由依赖于该传感器类型的任何操作系统功能使用。








