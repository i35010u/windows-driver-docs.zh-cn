---
title: 使用 DevCon 工具安装驱动程序包
description: 使用 DevCon 工具安装驱动程序包
ms.assetid: d77573e0-7866-46a5-88bc-c911bbd2a165
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e58b8cf9c61d1b21ae60adf366e07cfa741cb0e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545543"
---
# <a name="using-the-devcon-tool-to-install-a-driver-package"></a>使用 DevCon 工具安装驱动程序包


本主题中的示例使用*ToastPkg*示例[驱动程序包](driver-packages.md)。 在 WDK 安装目录中，包的源代码文件都位于*src\\常规\\toaster\\toastpkg\\toastcd*目录。 生成并进行数字签名的此驱动程序包后，将驱动程序包复制到目录*c:\\toaster*在测试计算机上。

若要安装驱动程序包通过 DevCon，执行以下操作：

1.  若要使用 DevCon 工具，用户必须是在测试计算机上 Administrators 组的成员并从提升的命令提示符运行 DevCon。 若要打开提升的命令提示符窗口，请创建桌面快捷方式*Cmd.exe*，右键单击*Cmd.exe*快捷方式，然后选择**以管理员身份运行**。

2.  从提升的命令提示符窗口中，输入以下信息：

    ```cpp
    devcon.exe install c:\toaster\toastpkg.inf {b85b7c50-6a01-11d2-b841-00c04fad5171}\mstoaster
    ```

    此命令行指定驱动程序包的 INF 文件的位置 (*c:\\toaster\\toastpkg.inf*) 和 toaster 设备的硬件标识符 (ID)、 INF 文件中指定。

 

 





