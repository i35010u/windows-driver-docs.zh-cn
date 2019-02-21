---
title: 安装地理位置驱动程序示例
description: 地理位置驱动程序示例模拟硬件，因为没有自动安装的即插即用 n 播放功能。 相反，必须使用 Windows 实用工具，devcon.exe，以安装该示例。
ms.assetid: A08EA9B0-E1D6-47AE-BD89-C43D7D817DAF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40cca5ae13c929345f9409de21fcdf0a0043b125
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520729"
---
# <a name="installing-the-geolocation-driver-sample"></a>安装地理位置驱动程序示例

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

地理位置驱动程序示例模拟硬件，因为没有自动安装的即插即用 n 播放功能。 相反，必须使用 Windows 实用工具，devcon.exe，以安装该示例。

以下步骤概述了安装过程。

1.  请确保您的驱动程序生成且未出错。

2.  2. 启用测试签名通过运行命令"bcdedit /set testsigning 上"从提升的命令提示符。 （需要重新启动计算机之后启用测试签名。）
3.  将您的驱动程序的 DLL 和 INF 文件复制到单独的文件夹。

4.  查找两个辅助安装程序 DLL 文件 （已检查或免费） 从 redist/wdf/*处理器\_类型*安装 WDK 文件夹。 将这些文件复制到步骤 3 中创建的文件夹。 例如，如果您安装 WDK 驱动器 C 上，您可以复制 WUDFUpdate\_从 c: 01009.dll\\WinDDK\\*生成\#*\\redist\\wdf\\x86。

5.  运行 Devcon.exe。 可以在工具中找到此程序\\安装 WDK devcon 文件夹。 例如，对于名为 WDKExample 传感器，则键入：

    **devcon.exe 安装 WDKExample.inf"传感器\\WDKExample"**

    **请注意**  不使用 Devcon.exe 安装已发布的驱动程序。 此建议是仅用于测试。

     

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



