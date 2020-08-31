---
title: Windows 驱动程序签名教程
ms.assetid: B6F907DC-74DC-4BF3-A2F9-481AE706733C
description: 提供概述并详细说明对 Windows 的驱动程序二进制文件进行签名的步骤
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3aabfaf7f3b511f97f4288e4690ed24b34f01ef
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094809"
---
# <a name="windows-driver-signing-tutorial"></a>Windows 驱动程序签名教程


本教程提供了概述，并详细介绍了在一个合并位置对 Windows 的驱动程序二进制文件进行签名的步骤。 以下子主题介绍了该过程：

[测试签名](test-signing.md) 
[版本签名](release-signing.md) 
[驱动程序签名安装疑难解答](troubleshooting-driver-signing-installation.md)

## <a name="overview"></a>概述


从 Windows Vista 开始，Windows 基于 x64 的版本要求在内核模式（包括驱动程序）下运行的所有软件都要进行数字签名。

Microsoft 提供了以下两种对驱动程序进行数字签名的方法：

1.  [使用 microsoft 和 Microsoft 验证你的驱动程序](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) 将为其提供签名。 当驱动程序包通过认证测试时，可由 Windows 硬件质量实验室 (WHQL) 对其进行签名。 如果你的驱动程序包由 WHQL 进行签名，则可以通过 Windows 更新计划或其他 Microsoft 支持的分发机制来分发。
2.  供应商或驱动程序开发人员可从 Microsoft 授权的证书颁发机构 (CA) 获取软件发布证书 (SPC) ，并使用它自行对内核模式和用户模式二进制文件进行签名。

在系统启动期间启动驱动程序的情况下，系统加载程序 (Windows Vista 和更高版本的 Windows) 加载的驱动程序必须使用软件发行者证书 (SPC) 来嵌入签署其驱动程序二进制映像文件。

**注意**   必需的内核模式代码签名策略适用于 Windows Vista 和更高版本的 Windows 上运行的基于 x64 的系统的所有内核模式软件。 但是，Microsoft 鼓励发布者对所有内核模式软件进行数字签名，包括设备驱动程序 (包含32位系统) 的用户模式驱动程序。 Windows Vista 和更高版本的 Windows，请验证32位系统上的内核模式签名。 支持受保护媒体内容的软件必须进行数字签名，即使它是32位。

 

用户模式驱动程序（如打印机驱动程序）将在基于 x64 的计算机上安装和运行。 系统将在安装过程中向用户显示一个对话框，要求审批以安装驱动程序。 从 windows 8 及更高版本的 Windows 开始，除非也对这些驱动程序包进行了签名，否则安装将无法继续。

以下资源更详细地介绍了驱动程序签名：

-   主 [驱动程序签名](driver-signing.md) 主题
-   [内核模式代码签名演练](/previous-versions/windows/hardware/design/dn653569(v=vs.85))中的 "如何对内核模块进行发布签名" 副标题介绍了对内核模式代码进行签名时应了解的内容。 文档中的信息也适用于对用户模式驱动程序进行签名。
-   Windows 7 WDK 中的 selfsign_readme.htm 文件位于 WDK 安装目录 \\ WinDDK \\ 7600.16385.1 \\ src \\ general \\ build \\ driversigning。 此目录还包含命令文件 selfsign_example .cmd，可以编辑该文件以运行驱动程序签名命令。 Windows 8.1 WDK 中的 selfsign_readme.htm 文件位于 C： \\ Program Files (x86) \\ Windows 工具包 \\ 8.1 \\ bin \\ selfsign 中，并提供指向其他驱动程序签名信息的链接。

 

