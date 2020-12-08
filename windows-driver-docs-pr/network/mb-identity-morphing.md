---
title: MB 标识变形简介
description: 描述用于 MB 设备驱动程序的标识变形的简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5ef6be0e0b5f22222371ee5577e6dee832a7165
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798089"
---
# <a name="introduction-to-mb-identity-morphing"></a>MB 标识变换简介


## <a name="identity-morphing"></a>标识变形


移动宽带 USB 硬件保护程序解决方案无需通过单独的媒体（如 cd-rom) ）将移动宽带和其他 IHV 功能的驱动程序包分发到 (，方法是在 USB 设备本身包含驱动程序包。

当首次在 Windows 中插入此类设备时，该设备会将其自身显示为大容量存储，这将导致向用户显示 Windows 自动播放对话框。 此时，设备不会向主机公开任何其他函数（大容量存储函数除外），以防止因缺少驱动程序软件而使用户出现的其他功能无法正常工作。 用户可以运行由 IHV 提供的软件来安装驱动程序包。 除了安装驱动程序包之外，由 IHV 提供的软件还推移设备向用户公开其他功能。

在 Windows 8 中插入时使用上述机制的移动宽带设备将作为大容量存储出现。 由于 Windows 8 对符合 MBIM 规范的移动宽带功能提供本机支持，因此，用户无需安装驱动程序包即可使用移动宽带功能。 本节中的子主题提供有关如何针对 Windows 8 实施此解决方案以允许用户使用移动宽带设备而无需安装驱动程序包的相关指导。

显示变形行为的移动宽带设备在本部分的子主题中称为变形设备。

[MB 标识变形解决方案概述](mb-identity-morphing-solution-overview.md) 
[MB 标识变形解决方案详细信息](mb-identity-morphing-solution-details.md)
 

 





