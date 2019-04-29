---
title: 传感器 ACPI 条目
description: 本主题介绍高级的配置和特定于 Windows 10 中的传感器的电源管理接口 (ACPI) 条目。
ms.assetid: DFDD5603-18F5-4F6C-8D09-D6905587F3CE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215ad91ae452a7ee55578701273a17eef2a4d500
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368771"
---
# <a name="sensors-acpi-entries"></a>传感器 ACPI 条目


本主题介绍高级的配置和特定于 Windows 10 移动版中的传感器的电源管理接口 (ACPI) 条目。 这些项时将添加到 ACPI 源语言 (ASL) 文件。

## <a name="rotm"></a>ROTM


旋转矩阵 (ROTM) 是用于描述传感器的 X、 Y 和 Z 轴和移动设备的 X、 Y 和 Z 轴之间的关系 （如 OEM 所定义） 的矩阵。

每一行表示分别应用到 X、 Y 和 Z 轴的转换。 每个条目是介于-1 和 1，最多 3 个小数位数可以拥有的每个数字的十进制数字。

例如，在以下**方法**，矩阵指示沿 Y，是传感器硬件的 X、 Y 和 Z 轴的 X 和 Z 轴的移动设备，分别。

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


以下**方法**将标记为主要的传感器。

```cpp
Method(PRIM, 0x0, NotSerialized) {
                Name(RBUF, Buffer(){1})
                    Return (RBUF)
            }
```

>[!NOTE]
> 如果有多个相同类型 （例如，多个加速感应器），在移动设备上的传感器，则必须将其中一个标记为主要使用**PRIM**关键字。 传感器的 GetDefault 方法调用时，将由 WinRT API 使用主传感器。 主传感器还将使用任何操作系统功能依赖于该传感器类型。








