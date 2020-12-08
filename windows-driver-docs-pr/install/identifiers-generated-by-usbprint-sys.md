---
title: USBPRINT.SYS 生成的标识符
description: USBPRINT.SYS 生成的标识符
keywords:
- USBPRINT.SYS WDK 设备安装
- 兼容 Id WDK 设备安装
- USB 打印驱动程序 WDK 设备安装
- 打印驱动程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 798862aedfea2a0eb13eba6c2d3a299d7da7db79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817745"
---
# <a name="identifiers-generated-by-usbprintsys"></a>USBPRINT.SYS 生成的标识符





从 Windows 2000 开始，操作系统提供了一个内核模式 USB 打印驱动程序， *usbprint.sys* 将打印机子系统连接到 USB 堆栈。 本机 USB 打印机驱动程序使供应商不必开发自己的内核模式 USB 打印机驱动程序。 这允许供应商开发高级用户模式打印机驱动程序，使用 USB 和并行打印机。

*Usbprint* 安装文件包含与所有 USB class 7 打印机设备匹配的兼容 ID。 如果 USB 集线器驱动程序枚举其中的一个设备，则操作系统将发现该集线器驱动程序在 *usbprint* 中生成的 ID 匹配，并将加载 USB 打印机驱动程序， *usbprint.sys*。 在 *usbprint* 中找到的兼容 ID 的格式如下：

USB \\ CLASS_07

其中：

-   类 07h = 属于 USB printer 类的设备

加载后，USB 打印机驱动程序将为打印机设备创建一个新的 PDO。 当即插即用 (PnP) 管理器查询新创建的 PDO 的设备标识字符串时，USB 打印机驱动程序将创建一个新的硬件 ID，该 ID 派生自设备的 IEEE 1284 字符串，该 ID 与并行总线枚举器生成的字符串标识符兼容。 此硬件 ID 的格式如下：

USBPRINT \\ NameModel (20) 校验和 (4) 

其中：

-   *NameModel (20)* 是制造商名称和设备型号的串联，最多可被截断为20个字符。

-   *校验和 (4)* 为4个字符的循环冗余检查 (CRC) 从制造商名称和型号名称计算的代码。

字符串中的空格将替换为下划线。 例如，如果制造商的名称为 "Hewlett-Packard"，则模型名称为 "HP Color LaserJet 550"，校验和为3115，则硬件 ID 如下所示：

USBPRINT \\ Hewlett-PackardHP_Co3115

在前面的示例中，模型名称中 "HP" 和 "Color" 之间的空间被替换为下划线，以生成截断的 make/model 字符串 "Hewlett-PackardHP_Co"。

**注意**  操作系统生成的 CRC 可能与上一节中所述的 CRC 或任何其他 CRC 算法都不匹配。 因此，打印机驱动程序可能无法计算正确的 hardwareID，无法与打印机驱动程序的 INF 文件一起使用。
若要检索 hardwareID，更好的做法是，搜索与正在安装的 USB 打印机关联的 setupapi.log 文件。

 

 

 





