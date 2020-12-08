---
title: 安装增强的存储证书管理工具
description: 安装增强的存储证书管理工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e4d235623c0aa1b5fa92c003ee34300aed44ddf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824625"
---
# <a name="installation-of-the-enhanced-storage-certificate-management-tool"></a>安装增强的存储证书管理工具


增强的存储证书管理工具可用于运行 Windows 7 和更高版本 Windows 的基于 x86、基于 Itanium 和 x64 的计算机。 若要在计算机上安装增强的存储证书管理工具，请完成以下步骤：

1.  将 EhStorCertMgrCmd.exe 从 WDKPath \\ tools \\ EnhancedStorage \\ ProcessorArchitecture 复制到 \\ 计算机上的% SystemRoot% System32，其中：

    -   *WDKPath* 是安装了 Windows 驱动程序工具包 (WDK) 的目录的路径。
    -   *ProcessorArchitecture* 是要在其上安装和运行增强的存储证书管理工具的计算机的处理器体系结构。 WDK 在 \\ \\ WDKPath 目录下的 tools EnhancedStorage amd64、tools \\ EnhancedStorage \\ i386 和 tools \\ EnhancedStorage \\ ia64 子目录 *WDKPath* 中安装文件的处理器特定版本。

    例如，如果测试计算机运行的是32位版本的 Windows，则必须将 tools \\ EnhancedStorage \\ i386 \\EhStorCertMgrCmd.exe 复制到% SystemRoot% \\ System32 中。

2.  将 EhStorCertMgrComponent.dll 从 WDKPath \\ tools \\ EnhancedStorage \\ ProcessorArchitecture 复制到 \\ 计算机上的% SystemRoot% System32 中。

3.  将 EhStorCertMgrCmd.exe mui 和 EhStorCertMgrComponent.dll 中的 WDKPath \\ 工具 \\ EnhancedStorage ProcessorArchitecture 复制 \\ 到计算机上% SystemRoot% System32 中特定于区域设置的子目录 \\ 。

    例如，如果你的区域设置为美国，则必须将所有的 mui 文件复制到% SystemRoot% \\ System32 \\ en-us。

4.  单击“启动”。

5.  右键单击 " **命令提示符** "，然后单击 " **以管理员身份运行**"。

6.  在命令提示符窗口中键入以下命令：
    ```
    regsvr32 /s %SystemRoot%/System32/EhStorCertMgrComponent.dll
    ```

**注意**  增强的存储证书管理工具的文件可以复制并安装在未安装 WDK 的其他计算机上。

 

 

 





