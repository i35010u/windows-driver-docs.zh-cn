---
title: 供应商提供的设备安装组件
description: 供应商提供的设备安装组件
ms.assetid: d86bdf75-9726-4b44-8753-7e9c19e88a61
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9ccabaafab72081086a69b9bcee7b834eaf6a4
ms.sourcegitcommit: 3a51ae8db61be0e25549a5527ea3143e3025e82f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65455016"
---
# <a name="vendor-provided-device-installation-components"></a>供应商提供的设备安装组件


本主题介绍 IHV 或 OEM 提供的设备安装组件。

<a href="" id="driver-package"></a>驱动程序包  
一个[驱动程序包](driver-packages.md)必须为你的设备以支持在 Windows 下提供的所有软件组件都组成。 这些组件包括：

-   [INF 文件](overview-of-inf-files.md)，提供了有关设备和安装驱动程序。 有关详细信息，请参阅[创建一个 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff538378)。

-   一个[编录文件](catalog-files.md)，其中包含的数字签名[驱动程序包](driver-packages.md)。 有关详细信息，请参阅[数字签名](digital-signatures.md)。

-   设备的驱动程序。

<a href="" id="drivers"></a>驱动程序  
驱动程序允许系统与硬件设备进行交互。 Windows 将驱动程序的二进制文件 (.sys) 复制到 %systemroot%\\system32\\时安装设备驱动程序目录。 驱动程序所需的大多数设备。

有关详细信息，请参阅[选择驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff554652)。

有关 Windows 驱动程序的详细信息，请参阅[开始使用 Windows 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff554690)。

 

 





