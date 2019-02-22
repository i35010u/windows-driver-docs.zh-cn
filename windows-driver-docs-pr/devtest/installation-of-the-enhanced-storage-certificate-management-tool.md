---
title: 增强的存储证书管理工具的安装
description: 增强的存储证书管理工具的安装
ms.assetid: 1494a911-73a4-4a8c-a29d-aecb65c846dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c07f5baa2d88d3cd9ecd4453195721fc6f6947f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555109"
---
# <a name="installation-of-the-enhanced-storage-certificate-management-tool"></a>增强的存储证书管理工具的安装


增强型存储证书管理工具是可用于运行 Windows 7 和更高版本的 Windows 的基于 x86、 基于 Itanium 和基于 x64 的计算机。 若要在计算机上安装增强存储证书管理工具，请完成以下步骤：

1.  从 WDKPath 复制 EhStorCertMgrCmd.exe\\工具\\EnhancedStorage\\ProcessorArchitecture 到 %systemroot%\\System32 的计算机上，其中：

    -   *WDKPath*是安装 Windows Driver Kit (WDK) 的目录的路径。
    -   *ProcessorArchitecture*是将安装增强存储证书管理工具的计算机、 在上的运行的处理器体系结构。 WDK 的工具中安装文件的特定于处理器的版本\\EnhancedStorage\\amd64，工具\\EnhancedStorage\\i386，和工具\\EnhancedStorage\\ia64下面的子目录*WDKPath*目录。

    例如，如果测试计算机运行 Windows 的 32 位版本，则必须将工具复制\\EnhancedStorage\\i386\\EhStorCertMgrCmd.exe 到 %systemroot%\\System32。

2.  从 WDKPath 复制 EhStorCertMgrComponent.dll\\工具\\EnhancedStorage\\ProcessorArchitecture 到 %systemroot%\\的计算机上的 System32。

3.  从 WDKPath 复制 EhStorCertMgrCmd.exe.mui 和 EhStorCertMgrComponent.dll.mui\\工具\\EnhancedStorage\\到 %systemroot%中的区域设置特定的子目录的 ProcessorArchitecture\\上的 System32在计算机中。

    例如，如果您的区域设置是在美国，您必须将复制所有.mui 文件到 %systemroot%\\System32\\EN-US。

4.  单击“开始” 。

5.  右键单击**命令提示符**然后单击**以管理员身份运行**。

6.  在命令提示符下键入以下命令：
    ```
    regsvr32 /s %SystemRoot%/System32/EhStorCertMgrComponent.dll
    ```

**请注意**  可以复制和其他不具有安装 WDK 的计算机上安装增强存储证书管理工具的文件。

 

 

 





