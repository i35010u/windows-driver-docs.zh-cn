---
title: 驱动程序包的组件
description: 驱动程序包的组件
ms.assetid: 3e09b17f-9a62-43fd-be00-29fe2e6140c5
keywords:
- 组件 WDK
- 驱动程序包 WDK，组件
- WDK，组件的包
- WDK 驱动程序包文件
- 共同安装程序 WDK 设备安装驱动程序包
- 安装文件 WDK
- .sys 文件
- SYS 文件
- .cat 文件
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: f0b178b36b0646ba3850ac77abadc6c212ac39df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533959"
---
# <a name="components-of-a-driver-package"></a>驱动程序包的组件





以下组件所需安装和支持 Windows 操作系统上的设备：

<a href="" id="the-device-itself"></a>**在设备本身**  
如果你打算设计和构建新的设备，请按照硬件的行业标准。 如果您遵循这些标准，则更有可能，简化了的开发过程，同时降低支持成本。 不仅对于此类设备，并测试套件存在，而且在许多情况下，通用驱动程序存在适用于标准类型。 因此，您可能不需要编写新的驱动程序。

<a href="" id="the-driver-package-for-the-device"></a>**设备驱动程序包**  
驱动程序包包括必须提供以确保你的设备支持 Windows 的所有软件组件。 通常情况下，驱动程序包包含以下组件：

-   驱动程序文件

-   安装文件

-   其他文件

后面的驱动程序包的每个组件的简要说明。

### <a name="driver-files"></a>驱动程序文件

该驱动程序是包的提供用于设备的 I/O 接口的一部分。 通常情况下，驱动程序是一个动态链接库 (DLL) 使用。*sys*文件扩展名。 允许使用长文件名，除*引导启动驱动程序*。 当安装了设备时，Windows 会复制 *.sys*的文件 *%systemroot%\\system32\\驱动程序*目录。

支持特定设备所需的软件取决于设备的总线或端口连接到的功能。 Microsoft 提供了许多常见设备和与操作系统的几乎所有总线驱动程序。 如果你的设备可以由一个驱动程序提供服务，你可能需要编写仅特定于设备的*微型驱动程序*。 微型驱动程序处理代表系统提供的驱动程序的特定于设备的功能。 对于某些类型的设备，甚至微型驱动程序不是必要的。 例如，通常可以只安装文件支持的调制解调器。

### <a name="installation-files"></a>安装文件

除了在设备和驱动程序、 驱动程序包还包含一个或多个提供驱动程序安装的以下文件：

-   设备安装程序信息 (INF) 文件

    INF 文件包含的信息的[系统提供的设备安装组件](system-provided-device-installation-components.md)使用安装在设备的支持。 Windows 将此文件复制到 %*SystemRoot*%\\*inf*安装设备时的目录。 每个设备必须具有一个 INF 文件。

    有关详细信息，请参阅[提供 INF 文件](supplying-an-inf-file.md)。

-   驱动程序[目录 (.cat) 文件](catalog-files.md)

    驱动程序目录文件包含驱动程序包中每个文件的加密哈希。 Windows 使用这些哈希来验证包发布后对其不已被更改。 若要确保不会更改目录文件，它应该[进行数字签名](digital-signatures.md)。

    有关如何进行签名的驱动程序的信息，请参阅[公开发布的版本的签名驱动程序](signing-drivers-for-public-release.md)并[签名驱动程序开发和测试期间](signing-drivers-during-development-and-test.md)。

### <a name="other-files"></a>其他文件

驱动程序包还可以包含其他文件，例如设备安装应用程序、 设备图标、 设备属性页中，等等。 有关详情，请参阅以下主题：

[提供设备属性页](providing-device-property-pages.md)

[安装引导启动驱动程序](installing-a-boot-start-driver.md)

 

 





