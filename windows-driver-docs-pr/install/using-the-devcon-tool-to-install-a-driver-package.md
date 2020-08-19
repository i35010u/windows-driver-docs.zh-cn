---
title: 使用 DevCon 工具安装驱动程序包
description: 使用 DevCon 工具安装驱动程序包
ms.assetid: d77573e0-7866-46a5-88bc-c911bbd2a165
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9455eebfaf2f14cde29b44e29dcb66a84f89e503
ms.sourcegitcommit: f5222e608f2853003175244505d5daa3465ac6b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88615071"
---
# <a name="using-the-devcon-tool-to-install-a-driver-package"></a>使用 DevCon 工具安装驱动程序包


本主题中的示例使用 *toastpkg.inf* 示例 [驱动程序包](driver-packages.md)。 在 WDK 安装目录中，包的源文件位于 *src \\ general \\ toaster \\ toastpkg.inf \\ toastcd* 目录中。 构建此驱动程序包并对其进行了数字签名后，将驱动程序包复制到测试计算机上的目录 *c： \\ toaster* 。

若要通过 DevCon 安装驱动程序包，请执行以下操作：

1.  若要使用 DevCon 工具，用户必须是测试计算机上 Administrators 组的成员，并从提升的命令提示符运行 DevCon。 若要打开提升的命令提示符窗口，请创建 *Cmd.exe*的桌面快捷方式，选择并按住 (或右键单击 *Cmd.exe* 快捷方式) ，然后选择 " **以管理员身份运行**"。

2.  在提升的命令提示符窗口中，输入以下内容：

    ```cpp
    devcon.exe install c:\toaster\toastpkg.inf {b85b7c50-6a01-11d2-b841-00c04fad5171}\mstoaster
    ```

    此命令行指定在 INF 文件中指定的驱动程序包 INF 文件 (*c： \\ toaster) \\ toastpkg.inf* 和 toaster 设备的硬件标识符 (ID) 的位置。

 

 





