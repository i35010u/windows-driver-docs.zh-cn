---
title: 设备安装文件
description: 设备安装文件
ms.assetid: a4a53040-ff53-49ba-a4a5-aba5f13119ef
keywords:
- 设备安装程序 WDK 设备安装文件
- 设备安装 WDK，文件
- 安装 WDK，文件的设备
- WDK 设备安装文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87958f2aa78b5161a5d710a5e81286c5bfeea46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357860"
---
# <a name="device-installation-files"></a>设备安装文件





支持特定设备所需的软件取决于各类设备和在其中使用该设备的方式。 通常情况下，供应商提供了中的以下软件[驱动程序包](driver-packages.md)以支持设备：

<a href="" id="a-device-setup-information-file--inf-file-"></a>设备安装程序信息文件 （INF 文件）  
INF 文件包含用于安装设备的支持系统的 Windows 组件的信息。 Windows 将此文件复制到 %*SystemRoot*%\\*inf*时它将安装驱动程序的目录。 此文件是必需的。

有关详细信息，请参阅[创建一个 INF 文件](overview-of-inf-files.md)。

<a href="" id="one-or-more-drivers-for-the-device"></a>一个或多个设备驱动程序  
答:。*sys*文件是驱动程序的图像文件。 Windows 将对此文件复制 *%systemroot%\\system32\\驱动程序*时安装该驱动程序的目录。 驱动程序所需的大多数设备。

有关详细信息，请参阅[选择驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff554652)。

<a href="" id="digital-signatures-for-the-driver-package--a-driver-catalog-file-"></a>数字签名的[驱动程序包](driver-packages.md)（驱动程序目录文件）  
驱动程序目录文件包含数字签名。 应签名的所有驱动程序包。

供应商提交其驱动程序包向 Windows 硬件质量实验室 (WHQL) 测试和签名，以获取数字签名。 WHQL 返回包具有编录文件 (。*cat*文件)。

有关详细信息，请参阅[WHQL 版本签名](whql-release-signature.md)。

<a href="" id="other-files"></a>其他文件  
一个[驱动程序包](driver-packages.md)可以包含其他文件，如自定义设备安装应用程序、 一个设备的图标或驱动程序库文件 （例如视频驱动程序）。

有关详细信息，请参阅[提供的设备属性页](providing-device-property-pages.md)并[具有特殊的安装要求的驱动程序](drivers-with-special-installation-requirements.md)。

此外，请参阅 WDK 中的特定于设备的类型的文档。

WDK 包括各种示例安装文件。 有关详细信息，请参阅[示例设备安装文件](sample-device-installation-files.md)

 

 





