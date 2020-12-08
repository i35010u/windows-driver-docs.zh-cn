---
title: 改进的彩色打印
description: 改进的彩色打印
keywords:
- XPSDrv 打印机驱动程序 WDK，彩色打印
- 彩色打印 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5938cea94fc96d1663ed4a0ae4c7d49eb70398b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796763"
---
# <a name="improved-color-printing"></a>改进的彩色打印


Windows Vista 中的新颜色管理功能和 XPS 打印路径一起使用，可提供更丰富、更可预测的颜色打印。 增强的颜色支持通过支持具有超过四个 colorants 的打印来实现高端打印。  (具有印前应用程序的客户需要四个以上的 colorants。 ) 新的 XPS 打印体系结构可以将应用程序生成的扩展颜色信息传递到广角彩色打印机。 设备驱动程序可以访问和控制打印管道内的颜色信息。

Windows Vista 充分利用 Windows 颜色系统，该系统对颜色管理进行了重大创新，以与不同软件应用程序、图像设备、图像媒体上的颜色相匹配，并以可预测、可靠且一致的方式查看条件。 XPS 文档是用于将应用程序颜色信息发送到基于 XPS 文档的设备的管道。 XPS 文档格式通过对以下项的本机支持应用此技术：

-   更高的精度、更高的动态范围和更大的色域颜色空间。

-   使用 CMYK 和支持 n-ink 系统 (，) 4 个 colorants 以上。

-   支持命名的颜色。

通过 XPS 假脱机文件，XPS 打印路径直接将此高级颜色信息传递到设备驱动程序。 设备驱动程序还可以提供以下改进的颜色处理：

-   具有 XPS 打印路径驱动程序的设备的自动颜色配置。

-   为不同打印设备重复使用管道中的内容的功能。

-   能够可靠地将颜色数据从应用程序保存到驱动程序，因为颜色配置文件和处理指令可以直接嵌入到假脱机文件中。

-   改善了颜色功能和设置的通信。 应用程序可以通过启用或禁用新打印路径中的系统颜色管理来控制颜色处理。 驱动程序可以更全面地了解其设备的颜色功能。

 

 




