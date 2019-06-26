---
title: Windows 驱动程序签名教程
ms.assetid: B6F907DC-74DC-4BF3-A2F9-481AE706733C
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac34c95f5e16cb48b8b434744b76c5136be9f408
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387301"
---
# <a name="windows-driver-signing-tutorial"></a>Windows 驱动程序签名教程


本教程提供了概述，并详细介绍的步骤来注册在一个统一的位置的 Windows 驱动程序二进制文件。 以下子主题介绍的过程：

[测试签名](test-signing.md)
[版本签名](release-signing.md)
[疑难解答驱动程序签名安装](troubleshooting-driver-signing-installation.md)
[相关主题和附录](related-topics-and-appendices.md)
## <a name="overview"></a>概述


从 Windows Vista 开始，基于 x64 的 Windows 版本所需的所有软件运行在内核模式下，其中包括驱动程序，以进行数字签名，这样才能加载。

Microsoft 提供的以下两种方法进行数字签名的驱动程序：

1.  [认证您的驱动程序与 Microsoft](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) ，Microsoft 将为其提供一个签名。 当驱动程序包通过认证测试时，可由 Windows 硬件质量实验室 (WHQL) 对其进行签名。 如果你的驱动程序包由 WHQL 进行签名，则可以通过 Windows 更新计划或其他 Microsoft 支持的分发机制来分发。
2.  供应商或驱动程序开发人员可以从 Microsoft 获取的软件发布证书 (SPC) 授权证书颁发机构 (CA)，并使用它进行签名本身的内核模式和用户模式的二进制文件。

在引导启动的情况下在系统期间的驱动程序启动，由系统加载程序 （Windows Vista 和更高版本的 Windows） 加载的驱动程序、 供应商必须使用嵌入登录到软件发布者证书 (SPC) 其驱动程序二进制图像文件。

**请注意**  必需的内核模式代码签名策略适用于 Windows Vista 和更高版本的 Windows 上运行的基于 x64 的系统的所有内核模式软件。 但是，Microsoft 鼓励发布者进行数字签名所有内核模式软件，适用于 32 位系统也包括设备驱动程序 （包括用户模式驱动程序）。 Windows Vista 和更高版本的 Windows，验证在 32 位系统上的内核模式下签名。 支持受保护的媒体内容的软件必须进行数字签名，即使它是 32 位。

 

用户模式驱动程序，如打印机驱动程序将安装和基于 x64 的计算机中工作。 一个对话框，将向用户显示要求批准来安装该驱动程序的安装过程。 从 Windows 8 和更高版本的 Windows 中，安装将无法继续除非这些驱动程序包也经过了签名。

以下资源中更详细地介绍驱动程序签名：

-   主[驱动程序签名](driver-signing.md)主题
-   子主题"如何为版本登录内核模块"中[内核模式代码签名演练](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653569(v=vs.85))描述您应了解的有关内核模式代码签名。 文档中的信息也适用于用户模式驱动程序签名。
-   在 Windows 7 WDK selfsign_readme.htm 文件位于 WDK 安装目录\\WinDDK\\7600.16385.1\\src\\常规\\生成\\driversigning。 此目录也有一个命令文件，selfsign_example.cmd，可以对其进行编辑，以便运行驱动程序签名的命令。 在 Windows 8.1 WDK selfsign_readme.htm 文件位于 c:\\Program Files (x86)\\Windows 工具包\\8.1\\bin\\selfsign，并提供指向其他驱动程序签名的信息。

 

 





