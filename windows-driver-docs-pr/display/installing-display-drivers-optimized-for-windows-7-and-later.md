---
title: 显示驱动程序的安装要求
description: 针对 Windows 7 和更高版本优化的显示驱动程序的安装要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d909f5af25c53879085cc24e8ce20c8d6a80b5b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839285"
---
# <a name="installation-requirements-for-display-drivers-optimized-for-windows-7-and-later"></a>针对 Windows 7 和更高版本优化的显示驱动程序的安装要求


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

对于写入 Windows 显示驱动程序模型 (WDDM) 并且已针对 Windows 7 及更高版本进行了优化的显示驱动程序，任何 INF 文件都必须符合 [显示微型端口和 User-Mode 显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)中所述的几个要求。 最值得注意的更改是 **FeatureScore** 指令。

以下要求是从 Windows 7 开始显示驱动程序 INF 文件的新要求：

[设置 Windows 7 显示驱动程序的功能评分](setting-the-feature-score-for-windows-7-display-drivers.md)

[将信息附加到 Windows 7 显示驱动程序的友好字符串名称](appending-information-to-the-friendly-string-names-for-windows-7-displ.md)

[区分 Windows 7 显示驱动程序的 SKU](differentiating-the-sku-for-windows-7-display-drivers.md)

[以 Unicode 格式编码 Windows 7 显示驱动程序 INF 文件](encoding-windows-7-display-driver-inf-files-in-unicode.md)

 

 





