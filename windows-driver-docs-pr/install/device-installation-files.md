---
title: 设备安装文件
description: 设备安装文件
ms.assetid: a4a53040-ff53-49ba-a4a5-aba5f13119ef
keywords:
- 设备设置 WDK 设备安装，文件
- 设备安装 WDK，文件
- 安装设备 WDK，文件
- 文件 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db76e33bee19d28014913ad1d517e31365ae155
ms.sourcegitcommit: f6aebb32c045b9da7da4bf9b3fd8d6fad05e9deb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "77089210"
---
# <a name="device-installation-files"></a>设备安装文件





支持特定设备所需的软件取决于设备的类型和使用设备的方式。 通常，供应商在[驱动程序包](driver-packages.md)中提供以下软件，以支持设备：

* <a href="" id="a-device-setup-information-file--inf-file-"></a>设备安装信息文件（INF 文件）  
    INF 文件包含系统 Windows 组件用于安装设备支持的信息。 Windows 在安装驱动程序时，会将此文件复制到%*SystemRoot*%\\*inf*目录。 此文件是必需的。

    有关详细信息，请参阅[创建 INF 文件](overview-of-inf-files.md)。

* <a href="" id="one-or-more-drivers-for-the-device"></a>设备的一个或多个驱动程序  
    的.*sys*文件是驱动程序的映像文件。 安装驱动程序时，Windows 会将此文件复制到 *% SystemRoot%\\system32\\驱动程序*目录。 大多数设备都需要驱动程序。

    有关详细信息，请参阅[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。

* <a href="" id="digital-signatures-for-the-driver-package--a-driver-catalog-file-"></a>[驱动程序包](driver-packages.md)的数字签名（驱动程序目录文件）  
    驱动程序目录文件包含数字签名。 所有驱动程序包都应进行签名。

    供应商通过向 Windows 硬件质量实验室（WHQL）提交用于测试和签名的驱动程序包来获取数字签名。 WHQL 返回包含目录文件（.*cat*文件）。

    有关详细信息，请参阅[WHQL 发行版签名](whql-release-signature.md)。

* <a href="" id="other-files"></a>其他文件  
    [驱动程序包](driver-packages.md)可以包含其他文件，如自定义设备安装应用程序、设备图标或驱动程序库文件（如视频驱动程序）。

    有关详细信息，请参阅提供[具有特殊安装要求的](drivers-with-special-installation-requirements.md)[设备属性页](providing-device-property-pages.md)和驱动程序。

另请参阅 WDK 中特定于设备类型的文档。

WDK 包括各种示例安装文件。 有关详细信息，请参阅[示例设备安装文件](sample-device-installation-files.md)

 

 





