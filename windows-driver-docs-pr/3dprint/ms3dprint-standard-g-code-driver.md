---
title: MS3DPrint 标准 G-Code 驱动程序
description: MS3DPrint 标准 G 代码驱动程序实现典型的 Windows 8.1 或 Windows 10 驱动程序以使用 G 代码（特别是开源打印机，其中包括来自 RepRap 项目的 filament）制造3D 打印机。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d05879abc1bca8ddee032b79e7996ceab71d4ad4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788121"
---
# <a name="ms3dprint-standard-g-code-driver"></a>MS3DPrint 标准 G-Code 驱动程序


MS3DPrint 标准 G 代码驱动程序实现了通用 Windows 8.1 或更高版本的带外 filament 制造3D 打印机的驱动程序，该驱动程序是使用 G 代码（特别是开源打印机，包括从 RepRap 项目派生的打印机）运行的。

此驱动程序集包含用于实现无线协议的 USB 驱动程序和用于将几何转换为刀具路径的切片器。 切片器驱动程序接收来自 Windows 后台处理程序的3MF 数据，并输出 USB 驱动程序的 G 代码。 USB 驱动程序通过串行连接一次发送一个指令，一次发送一个指令。 

USB 驱动程序和切片器均处于积极开发下，并且在将来的版本中可能会有所更改。  这些驱动程序集在 Windows 更新上发布，并自动提供给受支持的设备或设备，这些设备或设备使用 MS_COMP_3DPRINT USB 描述符声明自己的3D 打印机。
 

## <a name="3d-printing-sdk-driver-folder-contents"></a>3D 打印 SDK 驱动程序文件夹内容


下表提供了有关3D 打印 SDK 中驱动程序、切片器和呈现筛选器的位置的信息。

| Folder                    | 目录                                 |
|---------------------------|------------------------------------------|
| \\装箱                     | 已编译二进制文件                        |
| \\Bin \\ MS3DPrintUSB \_ x64  | 64位 USB 串行端口驱动程序包    |
| \\Bin \\ MS3DPrintUSB \_ x86  | 32位 USB 串行端口驱动程序包    |
| \\Bin \\ RenderFiltersV4 \_ x64 | 64位切片器和呈现筛选器包 |
| \\Bin \\ RenderFiltersV4 \_ x86 | 64位切片器和呈现筛选器包 |

 

## <a name="in-this-section"></a>在本节中


[驱动程序安装](driver-installation.md)

[配置设备](configuring-the-device.md)

[切片器设置](slicer-settings.md)

[示例配置 XML](sample-configuration-xml.md)

 




