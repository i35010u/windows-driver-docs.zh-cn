---
title: MB 标识变形
description: 描述标识变形的 MB 设备驱动程序
ms.assetid: 7AA14A5E-47AA-4A9A-94A4-769F374EA465
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9056d312c7b278aed582d28342b2f2aed17f26f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568165"
---
# <a name="mb-identity-morphing"></a>MB 标识变换


## <a name="identity-morphing"></a>标识变形


移动宽带 USB 硬件保护装置解决方案通过 USB 设备本身，其中包含驱动程序包中具有存储函数不再需要分发驱动程序包移动宽带和其他 IHV 函数，通过独立媒体 （如 CD-ROM)。

第一个时间插入时的 Windows 中的此类设备，设备将自己呈现为大容量存储，在 Windows 自动播放对话框的结果显示给用户。 此时，设备公开到除大容量存储函数主机，以防止其他函数的用户为非功能性由于缺少驱动程序软件使其不显示任何其他函数。 用户可以运行安装驱动程序包的 IHV 提供软件。 除了安装驱动程序包，IHV 提供软件还采用设备公开给用户的其他函数。

使用前面所述的机制时插入到 Windows 8 中的移动宽带设备将显示为大容量存储。 因为 Windows 8 提供了对符合 MBIM 规范，安装驱动程序包的移动宽带函数不需要用户以使用移动宽带功能。 在本部分中的子主题提供有关如何实现此解决方案为 Windows 8，以允许用户使用移动宽带设备而无需安装驱动程序包到 Ihv 指导。

移动宽带设备显示变形行为被称为变形设备在本部分中的子主题。

[MB 标识变形解决方案概述](mb-identity-morphing-solution-overview.md)
[MB 标识变形解决方案的详细信息](mb-identity-morphing-solution-details.md)
 

 





