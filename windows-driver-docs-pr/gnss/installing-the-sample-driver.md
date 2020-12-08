---
title: 安装地理位置驱动程序示例
description: 由于地理位置驱动程序示例模拟硬件，因此没有可用于自动执行安装的即插即用功能。 相反，必须使用 Windows 实用程序 devcon.exe 来安装该示例。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34105f258ddef1a2f31616942c0c314ac19eb469
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837299"
---
# <a name="installing-the-geolocation-driver-sample"></a>安装地理位置驱动程序示例

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

由于地理位置驱动程序示例模拟硬件，因此没有可用于自动执行安装的即插即用功能。 相反，必须使用 Windows 实用程序 devcon.exe 来安装该示例。

以下步骤概述了安装过程。

1.  请确保你的驱动程序生成时没有错误。

2.  2. 通过在提升的命令提示符下运行命令 "bcdedit/set testsigning on" 来启用测试签名。  (在启用测试签名后，需要重新启动计算机。 ) 
3.  将驱动程序的 DLL 和 INF 文件复制到一个单独的文件夹中。

4.  从安装了 WDK 的 "可再发行/wdf/*处理器 \_ 类型* " 文件夹 (选中或免费) 查找两个共同安装程序 DLL 文件。 将这些文件复制到你在步骤3中创建的文件夹。 例如，如果在驱动器 C 上安装了 WDK，则可以复制 WUDFUpdate \_01009.dll 从 C： \\ WinDDK \\ *\# build* \\ \\ \\

5.  运行 Devcon.exe。 可以在安装了 WDK 的 tools devcon 文件夹中找到此程序 \\ 。 例如，对于名为 WDKExample 的传感器，你可以键入：

    **devcon.exe 安装 WDKExample "传感器 \\ WDKExample"**

    **注意**  不要使用 Devcon.exe 来安装已发布的驱动程序。 此建议仅用于测试。

     

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



