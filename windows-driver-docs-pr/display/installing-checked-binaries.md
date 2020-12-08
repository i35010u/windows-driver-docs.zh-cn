---
title: 安装已检查的二进制文件
description: 安装已检查的二进制文件
keywords:
- 选中的二进制文件 WDK 显示
- 二进制文件 WDK 显示
- 免费二进制文件 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2450191784049129f7a6c5cdca53625fd1c2682f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827223"
---
# <a name="installing-checked-binaries"></a>安装已检查的二进制文件


为 Windows 显示驱动程序模型 (WDDM) 开发新的驱动程序时，应使用 WDDM 组件的已检查二进制文件。 这些组件的已检查二进制文件版本具有广泛的验证和调试辅助功能，这些辅助二进制文件并不提供这些功能。 不过，由于选中的二进制文件速度较慢，因此应将免费的二进制文件用于性能优化。

要运行 WDDM 的已检查二进制文件的硬件供应商可以使用下列方法之一：

-   安装 Windows Vista 或更高版本的已选择版本。 例如，如果要开发适用于 Windows 7 的驱动程序而不是 Windows Vista，则安装 Windows 7 的已选择二进制版本。

    这是最直接的方法。 但是，运行所有已全选的操作系统组件版本可能会导致总体性能下降。 因此，这并不总是正确的选择。

-   在 Windows Vista 或更高版本的免费版本上安装 WDDM 组件的已检查二进制版本。

    对于 WDDM，建议使用这种方法运行二进制文件。

    通过使用 Windows Vista 或更高版本的备用安装重新启动，将二进制 Windows Vista 或更高版本中的 WDDM 二进制文件替换为其选定的二进制版本。

    **注意**  *Win32k.sys*、 *Gdi32.dll*、 *Winsrv.dll* 和 *User32.dll* WDDM 二进制文件是此规则的例外情况。 这些二进制文件应始终与要安装的操作系统版本匹配。 因此，在操作系统的免费二进制版本中，这些二进制文件也应为免费二进制;在操作系统版本的已检查二进制版本中，这些二进制文件应为 checked 二进制。 否则，硬件供应商可以混合并匹配所有其他 WDDM 二进制文件的二进制和全选二进制版本。

     

 

 





