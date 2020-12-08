---
title: 供应商提供的设备安装组件
description: 供应商提供的设备安装组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b395f8fb376f2f9f1c31dcf8d4bc090efcf4187
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840951"
---
# <a name="vendor-provided-device-installation-components"></a>供应商提供的设备安装组件


本主题介绍了由 IHV 或 OEM 提供的设备安装组件。

<a href="" id="driver-package"></a>驱动程序包  
[驱动程序包](driver-packages.md)包含必须提供给在 Windows 下受支持的设备的所有软件组件。 这些组件包括：

-   [INF 文件](overview-of-inf-files.md)，提供有关要安装的设备和驱动程序的信息。 有关详细信息，请参阅 [创建 INF 文件](../hid/creating-an-inf-file.md)。

-   [目录文件](catalog-files.md)，其中包含[驱动程序包](driver-packages.md)的数字签名。 有关详细信息，请参阅 [数字签名](digital-signatures.md)。

-   设备的驱动程序。

<a href="" id="drivers"></a>驱动程序  
驱动程序允许系统与硬件设备交互。 安装设备后，Windows 会将驱动程序的二进制文件 ( .sys) 复制到% SystemRoot% \\ system32 \\ 驱动程序目录。 大多数设备都需要驱动程序。

有关详细信息，请参阅 [选择驱动程序模型](../gettingstarted/choosing-a-driver-model.md)。

有关 Windows 驱动程序的详细信息，请参阅 [Windows 驱动程序入门](../gettingstarted/index.md)。

 

