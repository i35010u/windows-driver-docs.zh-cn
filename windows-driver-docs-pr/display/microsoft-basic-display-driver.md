---
title: Microsoft 基本显示驱动程序
description: 在 Windows 8 中，Microsoft 基本显示器驱动程序 (MSBDD) 是替换 XDDM VGA 保存和 VGA PnP 驱动程序的内置显示器驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56ad38fa9de65800b3793cc6f2f396250b7abea5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840767"
---
# <a name="microsoft-basic-display-driver"></a>Microsoft 基本显示驱动程序


在 Windows 8 中，Microsoft 基本显示器驱动程序 (MSBDD) 是替换 XDDM VGA 保存和 VGA PnP 驱动程序的内置显示器驱动程序。

使用 MSBDD 的主要优点如下：

-   MSBDD 可帮助实现一致的最终用户和开发人员体验，因为它与 DirectX Api 和技术（如桌面组合）兼容。
-   服务器方案可以从更高的功能中受益 (具体而言，是由 WDDM 驱动程序模型提供的功能，例如无需重新启动的更新、动态启动和) 停止等功能。
-   MSBDD 支持统一可扩展固件接口 (UEFI) 图形输出协议 (GOP) 。
-   MSBDD 可在 XDDM 和 WDDM 硬件上工作。

MSBDD 是在安装过程中、在安全模式下、缺少 IHV 图形驱动程序时或在已禁用收件箱的图形 IHV 驱动程序的情况下加载的默认内置显示驱动程序。 此驱动程序的主要目的是使 Windows 能够写入显示控制器的线性帧缓冲区。

MSBDD 可以使用视频 BIOS 来管理单个监视器的模式和分辨率。 在 UEFI 平台上，MSBDD 继承在启动过程中设置的线性帧缓冲区;在这种情况下，不能更改模式或分辨率。 如 *Microsoft 基本显示器驱动程序所支持的方案* 所示，在以下情况下将使用 MSBDD：

-   服务器：缺少 WDDM 功能的图形硬件的服务器配置可以使用 MSBDD。
-   Windows 安装程序：在 Windows 安装程序的早期阶段，就在最终启动之前，只会加载 MSBDD。

    例如，用户的旧平台目前处于工作状态，但它没有适用于 Windows 8 的内置图形驱动程序支持。 用户升级到 Windows 8 并使用 MSBDD 进行设置、安装，并检索 IHV 驱动程序（如果有）。

-   驱动程序安装，在以下情况下：
    -   当用户安装新的 WDDM IHV 驱动程序时，将在从旧的 WDDM IHV 驱动程序卸载到) 安装新的 IHV 驱动程序之前的点时，从 (开始，使用 MSBDD。
    -   如果用户在安装最新的 WDDM IHV 驱动程序时遇到问题，则用户或系统可以禁用当前图形驱动程序并回退到使用 MSBDD。
-   驱动程序升级：通过使用 MSBDD，升级到 IHV 推荐的驱动程序时无需进行系统重新启动。
-   安全模式：在此模式下，只会加载受信任的驱动程序;其中包括 MSBDD。

![microsoft 基本显示器驱动程序支持的方案](images/scenariossupportedmicrosoftbasicdisplaydriver.jpg)

**图 1 Microsoft 基本显示器驱动程序支持的方案**

 

 





