---
title: 生成的 USBPRINT 的标识符。SYS
description: 生成的 USBPRINT 的标识符。SYS
ms.assetid: 23f71429-7318-4442-81b8-3818298cfd16
keywords:
- USBPRINT。SYS WDK 设备安装
- 兼容 Id WDK 设备安装
- USB 打印驱动程序 WDK 设备安装
- 打印驱动程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51e3c0a7530bdc6f60e4ca9f23c6e579d1efda09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525013"
---
# <a name="identifiers-generated-by-usbprintsys"></a>生成的 USBPRINT 的标识符。SYS





从 Windows 2000 开始，操作系统提供内核模式 USB 打印驱动程序， *usbprint.sys*打印机子系统连接到 USB 堆栈。 本机 USB 打印机驱动程序释放供应商开发他们自己内核模式 USB 打印机驱动程序的需要。 这允许开发高级用户模式打印机驱动程序供应商采用了 USB 和并行打印机。

*Usbprint.inf*安装文件包含兼容 ID 相匹配的所有 USB 类 7 打印机设备。 如果 USB 集线器驱动程序枚举这些设备之一，操作系统将查找中心驱动程序中生成的 ID 的匹配项*usbprint.inf*并且将加载 USB 打印机驱动程序*usbprint.sys*。 在中找到兼容 ID *usbprint.inf*具有以下形式：

USB\\CLASS_07

其中：

-   类 07 h = 属于 USB 打印机类的设备

只要将加载它，USB 打印机驱动程序会创建一个新的 PDO 打印机设备的。 USB 打印机驱动程序当插即用 (PnP) 管理器查询的新创建的 PDO 的设备标识字符串时，创建一个新的硬件 ID，派生自与生成的字符串标识符兼容的设备的 IEEE 1284 字符串并行总线枚举器。 此硬件 ID 的格式如下：

USBPRINT\\NameModel(20)Checksum(4)

其中：

-   *NameModel(20)* 是制造商名称的串联和设备，并截断为最多 20 个字符的模型。

-   *Checksum(4)* 4 个字符的循环冗余校验 (CRC) 代码计算从制造商名称和模型名称。

字符串中的空格替换为下划线。 例如，如果制造商的名称为"Hewlett-Packard"，模型名称为"HP 颜色 LaserJet 550"和校验和 3115，则硬件 ID 将按如下所示：

USBPRINT\\Hewlett-PackardHP_Co3115

在上一示例中，"HP"和"Color"之间的空间中的模型名称已替换为下划线以生成截断的制造商/型号字符串"Hewlett-PackardHP_Co。"

**请注意**  由操作系统生成的 CRC 可能与所述的前面部分中，或任何其他 CRC 算法计算的 CRC 不匹配。 因此，您的打印机驱动程序可能不能计算正确的硬件 Id 将用于打印机驱动程序 INF 文件。
若要检索的硬件 Id，它是更好地与正在安装的 USB 打印机关联 setupapi.dev.log 文件进行搜索。

 

 

 





