---
title: 显示器驱动程序的安装要求
description: 针对 Windows 7 和更高版本优化的显示驱动程序的安装要求
ms.assetid: 6dcf7c03-e39c-4c1c-b892-2e3e2c8c4b20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f5d0736cb652d1636d501a7824e29a345c8d15a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365462"
---
# <a name="installation-requirements-for-display-drivers-optimized-for-windows-7-and-later"></a>针对 Windows 7 和更高版本优化的显示驱动程序的安装要求


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

对于任何 INF 文件显示驱动程序编写为 Windows 显示驱动程序模型 (WDDM)，和的针对 Windows 7 进行了优化和中所述的几项要求更高版本，必须符合[显示微型端口的安装要求和用户模式显示驱动程序](installing-display-miniport-and-user-mode-display-drivers.md)。 最值得注意的更改是在**FeatureScore**指令。

新的显示驱动程序 INF 文件从 Windows 7 开始，还有下列要求：

[为 Windows 7 的显示器驱动程序设置功能分数](setting-the-feature-score-for-windows-7-display-drivers.md)

[将信息追加到 Windows 7 的显示器驱动程序的友好字符串名称](appending-information-to-the-friendly-string-names-for-windows-7-displ.md)

[Windows 7 的显示器驱动程序的区分 SKU](differentiating-the-sku-for-windows-7-display-drivers.md)

[Windows 7 的显示器驱动程序 INF 文件以 unicode 格式进行编码](encoding-windows-7-display-driver-inf-files-in-unicode.md)

 

 





