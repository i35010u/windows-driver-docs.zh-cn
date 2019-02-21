---
title: MS3DPrint 标准 G 代码驱动程序
description: MS3DPrint 标准 G 代码驱动程序实现的典型 Windows 8.1 或 Windows 10 驱动程序的浮点混合的 filament 制造 3D 打印机使用 G 代码运行，尤其是打开源打印机，包括那些从 RepRap 项目。
ms.assetid: F5818F58-C705-458F-9806-3F840BF7EE01
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa433689f8ccd56b7a494a019655a3995798a72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545191"
---
# <a name="ms3dprint-standard-g-code-driver"></a>MS3DPrint 标准 G 代码驱动程序


MS3DPrint 标准 G 代码驱动程序实现的通用 Windows 8.1 或更高版本的驱动程序的浮点混合的 filament 制造 3D 打印机使用 G 代码运行，尤其是打开源打印机，其中包含派生自 RepRap 项目。

此驱动程序集包含的 USB 驱动程序，实施 wire protocol 和切片器将几何图形转换为进行。 切片器驱动程序从 Windows 后台处理程序接收 3MF 数据和 G 代码输出的 USB 驱动程序。 USB 驱动程序通过串行连接发送一次 G 代码一条指令。 

USB 驱动程序和切片器是处于积极开发阶段和实现和规范的部分是将在未来版本中进行。  这些驱动程序的一组是发布在 Windows 更新上，自动提供给受支持的设备或设备声明本身 3D 打印机使用 MS_COMP_3DPRINT USB 描述符。
 

## <a name="3d-printing-sdk-driver-folder-contents"></a>3D 打印 SDK 驱动程序文件夹内容


下表提供有关驱动程序，切片器的位置的信息，并呈现 3D 打印 SDK 中的筛选器。

| 文件夹                    | 目录                                 |
|---------------------------|------------------------------------------|
| \\Bin                     | 编译的二进制文件                        |
| \\Bin\\MS3DPrintUSB\_x64  | 64 位 USB 串口驱动程序包    |
| \\Bin\\MS3DPrintUSB\_x86  | 32 位 USB 串口驱动程序包    |
| \\Bin\\RenderFiltersV4\_x64 | 64 位切片器和呈现器的筛选器包 |
| \\Bin\\RenderFiltersV4\_x86 | 64 位切片器和呈现器的筛选器包 |

 

## <a name="in-this-section"></a>本部分内容


[驱动程序安装](driver-installation.md)

[配置设备](configuring-the-device.md)

[切片器设置](slicer-settings.md)

[示例配置 XML](sample-configuration-xml.md)

 




