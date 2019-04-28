---
title: Microsoft 基本显示驱动程序
description: 在 Windows 8 中，Microsoft 基本显示驱动程序 (MSBDD) 是替换 XDDM VGA 保存和 VGA 即插即用驱动程序的框中显示驱动程序。
ms.assetid: CE89E02E-6527-4285-998B-618EE235CB8F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44770f53929f205f3a27915af8df440cefd5cd59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344625"
---
# <a name="microsoft-basic-display-driver"></a>Microsoft 基本显示驱动程序


在 Windows 8 中，Microsoft 基本显示驱动程序 (MSBDD) 是替换 XDDM VGA 保存和 VGA 即插即用驱动程序的框中显示驱动程序。

使用 MSBDD 的主要优点是，如下所示：

-   MSBDD 可帮助实现一致的最终用户和开发人员体验，因为它与 DirectX Api 和技术，例如桌面组合都兼容。
-   服务器方案可以受益于更高版本功能 （具体而言，等无重启的更新 （动态启动和停止） 和等等的功能） 提供的 WDDM 驱动程序模型。
-   MSBDD 支持统一可扩展固件接口 (UEFI) 的图形输出协议 (GOP)。
-   MSBDD 可以 XDDM 和 WDDM 的硬件上运行。

MSBDD 是默认值框中显示驱动程序安装过程中，在安全模式下，IHV 图形驱动程序，如果没有加载，或者在收件箱安装图形 IHV 驱动程序不起作用，或已禁用。 此驱动程序的主要用途是启用 Windows 写入显示控制器的线性帧缓冲区。

MSBDD 可以使用视频 BIOS 管理模式和一台监视器上的解决方法。 在 UEFI 平台上 MSBDD 继承在启动; 过程中设置的线性帧缓冲区在这种情况下，不不可能进行任何模式或分辨率更改。 如中所示*支持的 Microsoft 基本显示驱动程序的图 1 方案*，MSBDD 用于以下方案：

-   服务器：缺少支持 WDDM 的图形硬件的服务器配置可以使用 MSBDD。
-   Windows 安装程序：在 Windows 安装程序，就在最终启动之前的早期阶段被加载仅 MSBDD。

    例如，用户有一个较旧的平台，尽管它具有针对 Windows 8 支持没有现成图形驱动程序目前处于工作状态。 用户升级到 Windows 8 和 MSBDD 用于安装程序安装，并检索 IHV 驱动程序，如果一个可用。

-   驱动程序安装，在以下情况下：
    -   当用户正在安装新的 WDDM IHV 驱动程序时，MSBDD 使用 （从旧 WDDM IHV 驱动程序卸载到点之前安装了新的 IHV 驱动程序时的点） 转换的过程。
    -   当用户遇到安装最新的 WDDM IHV 驱动程序问题时，则可以禁用用户或系统的当前图形驱动程序和回退到使用 MSBDD。
-   驱动程序升级：通过使用 MSBDD，没有无需经历的系统重启时升级到 IHV 建议驱动程序。
-   安全模式：在此模式下，加载仅受信任的驱动程序;这包括 MSBDD。

![microsoft 基本显示驱动程序支持的方案](images/scenariossupportedmicrosoftbasicdisplaydriver.jpg)

**图 1 所支持的 Microsoft 基本显示驱动程序的方案**

 

 





