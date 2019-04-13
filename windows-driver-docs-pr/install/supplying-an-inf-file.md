---
title: 提供 INF 文件
description: 提供 INF 文件
ms.assetid: 208726d9-6f62-46a4-84a1-6fab3895bbe3
keywords:
- 驱动程序包 WDK、 INF 文件
- 包 WDK、 INF 文件
- INF 文件 WDK，有关 INF 文件
- 信息文件 WDK
- .inf 文件
- 设备安装 WDK、 INF 文件
- 安装设备 WDK、 INF 文件
- 设备安装 WDK、 INF 文件
- INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 222e73663b9d19edac1e57e92a76eaf3eeaf0eac
ms.sourcegitcommit: c340d6058fa3ea6407d0041de80482b88f623a90
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59534151"
---
# <a name="supplying-an-inf-file"></a>提供 INF 文件





每个驱动程序包必须包括 INF 文件，其中[设备安装组件](https://msdn.microsoft.com/library/windows/hardware/ff541277)读取安装设备时。 INF 文件不是安装脚本。 它是 ASCII 或 Unicode 文本文件，提供设备和驱动程序的信息，包括驱动程序文件、 注册表项，设备 Id[编录文件](catalog-files.md)，并安装该设备或驱动程序所需的版本信息。 不仅设备或驱动程序是首次安装时，而且还在一个驱动程序的用户请求更新通过设备管理器中，使用 INF。

确切内容和 INF 文件的格式取决于[设备安装程序类](device-setup-classes.md)。 [摘要的 INF 部分](summary-of-inf-sections.md)介绍每种类型的 INF 中所需的信息。 一般情况下，每个制造商信息是否位于[ **INF*模型*部分**](inf-models-section.md)。 中的条目**模型**部分是指[ **INF *DDInstall*部分**](inf-ddinstall-section.md)包含特定于模型的详细信息。

[InfVerif](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/infverif)中提供的工具*\\工具*目录的 Microsoft Windows Driver Kit (WDK)，检查语法和结构的所有跨类 INF 部分和指令中与打印机除外的所有安装程序类的特定于类的扩展。

从 Windows 2000 开始，可以使用用于在所有版本的 Windows 操作系统上安装一个 INF 文件。 有关详细信息，请参阅[创建多个平台和操作系统的 INF 文件](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。 如果将在国际市场中销售你的设备，则应该[创建国际 INF 文件](creating-international-inf-files.md)。 根据所涉及的位置，国际的 INF 文件可能需要将 Unicode 文件，而不是 ASCII。

创建您的驱动程序的 INF 文件的好方法是修改 WDK 提供的示例之一。 大部分 WDK 示例驱动程序的示例驱动程序所在的同一目录中包括 INF 文件。

有关 INF 文件的详细信息，请参阅[创建一个 INF 文件](overview-of-inf-files.md)，为文档[InfVerif](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/infverif)，WDK 和随附示例驱动程序的 INF 文件中的特定于设备的文档对于类似于你的设备。

 

 





