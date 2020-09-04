---
title: 驱动程序包的组件
description: 驱动程序包的组件
ms.assetid: 3e09b17f-9a62-43fd-be00-29fe2e6140c5
keywords:
- 组件 WDK
- 驱动程序包 WDK，组件
- 程序包 WDK，组件
- 文件 WDK 驱动程序包
- 共同安装程序 WDK 设备安装，驱动程序包
- 安装文件 WDK
- .sys 文件
- SYS 文件
- .cat 文件
ms.date: 05/09/2018
ms.localizationpriority: High
ms.openlocfilehash: 7987d58d9b4a198c9e8061a5a438b7a66f18e187
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094903"
---
# <a name="components-of-a-driver-package"></a>驱动程序包的组件





在 Windows 操作系统上安装和支持设备需要以下组件：

<a href="" id="the-device-itself"></a>**设备本身**  
如果计划设计和构建新设备，请遵循行业硬件标准。 遵循这些标准，更可能会简化开发过程并降低支持成本。 不仅为此类设备提供测试套件，而且在许多情况下，为标准类型提供通用驱动程序。 因此，可能无需编写新的驱动程序。

<a href="" id="the-driver-package-for-the-device"></a>**设备的驱动程序包**  
驱动程序包包括你必须提供的所有软件组件，以确保你的设备支持 Windows。 通常，驱动程序包中包含下列组件：

-   驱动程序文件

-   安装文件

-   其他文件

下面是对驱动程序包的每个组件的简短说明。

### <a name="driver-files"></a>驱动程序文件

驱动程序是为设备提供 I/O 接口的程序包的一部分。 通常，驱动程序是带有 sys  文件扩展名的动态链接库 (DLL)。 允许使用长文件名，启动驱动程序  除外。 安装设备后，Windows 会将 .sys  文件复制到 %SystemRoot%\\system32\\ 驱动程序  目录。

支持特定设备所需的软件取决于设备的功能，以及它所连接到的总线或端口。 随操作系统一起，Microsoft 为许多常用设备和几乎所有的总线都附带了驱动程序。 如果这些驱动程序之一可以为你的设备提供服务，则可能只需要编写设备特定的微型驱动器  。 微型驱动器代表系统提供的驱动程序处理设备特定的功能。 对于某些类型的设备，甚至不需要微型驱动器。 例如，通常可以仅通过安装文件来支持调制解调器。

### <a name="installation-files"></a>安装文件

除了设备和驱动程序外，驱动程序包还包含以下一个或多个提供驱动程序安装的文件：

-   设备安装程序信息 (INF) 文件

    INF 文件包含[系统提供的设备安装组件](system-provided-device-installation-components.md)用于安装设备支持的信息。 安装设备时，Windows 将此文件复制到 %SystemRoot  %\\inf  目录。 每个设备都必须有一个 INF 文件。

    有关详细信息，请参阅[提供 INF 文件](supplying-an-inf-file.md)。

-   驱动程序[目录 (.cat) 文件](catalog-files.md)

    驱动程序目录文件包含驱动程序包中每个文件的加密哈希。 Windows 使用这些哈希值来验证程序包在发布后是否未被更改。 若要确保不更改目录文件，应[使用数字签名](digital-signatures.md)。

    有关如何对驱动程序进行签名的信息，请参阅[对驱动程序的公共版本签名](signing-drivers-for-public-release--windows-vista-and-later-.md)，以及[在开发和测试期间对驱动程序签名](./introduction-to-test-signing.md)。

### <a name="other-files"></a>其他文件

驱动程序包还可以包含其他文件，如设备安装应用程序、设备图标、设备属性页等。 有关详情，请参阅以下主题：

[为设备提供图标](providing-vendor-icons-for-the-shell-and-autoplay.md)

[安装引导启动驱动程序](installing-a-boot-start-driver.md)