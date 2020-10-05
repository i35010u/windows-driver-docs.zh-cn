---
title: WDDM 1.2 最佳做法
description: 为了在 Windows 8 及更高版本中提供最佳体验，Windows 利用了与 Windows 显示驱动程序模型（ (WDDM) 1.2 或更高版本的驱动程序）配对的图形硬件。 本部分总结了最佳实践。
ms.assetid: 130C66F0-1ACE-4C6E-AE16-AEFCD4847312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 223ffab85bb2f5b48911949f08495e5bd95a23d8
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734467"
---
# <a name="wddm-12-best-practices"></a>WDDM 1.2 最佳做法


为了在 Windows 8 及更高版本中提供最佳体验，Windows 利用了与 Windows 显示驱动程序模型（ (WDDM) 1.2 或更高版本的驱动程序）配对的图形硬件。 本部分总结了最佳实践。

**系统制造商：**

-   请确保以下事例经过全面测试，并与系统配置配合使用：
    -   与 Microsoft 基本显示器驱动程序兼容
    -   不需要重新启动的服务器上的更新
-   用 WDDM 硬件设计新的服务器，并采用最适合客户需求的相关 WDDM 驱动程序类型。
-   与图形硬件供应商合作，以获取经过认证的 WDDM 1.2 驱动程序用于验证。
-   对于无外设系统：
    -   系统固件应在固定 ACPI 说明表的 "IAPC BOOT" 字段中设置 "VGA Not in" 标志 \_ \_ ， (FADT) ，如果有任何 VBIOS，则它应通过 VESA BIOS 扩展 (VBE) 实现空模式列表。
    -   在缺少 VBE 支持的情况下，无外设系统不应通过统一可扩展固件接口 (UEFI) 图形输出协议 (GOP) 来表示工作显示。
-   请参阅 [Windows 硬件认证](/previous-versions/windows/hardware/hck/jj124227(v=vs.85)) ，验证和测试信息。
-   在台式计算机和移动系统上测试各种硬件配置，以确保在 Windows 8 及更高版本上获得坚实的最终用户体验。

**图形硬件供应商：**

-   与 Microsoft 合作开发 WDDM 1.2 驱动程序。
-   测试 Windows 8 及更高版本上预发行的 WDDM 1.2 驱动程序。
-   通过 Windows 更新向 Microsoft 提供更新的 WDDM 1.x 驱动程序以进行部署。
-   除了 Windows 认证测试套件外，还可以验证每个 ASIC 系列上的图形和游戏性能、应用程序兼容性以及各种自主机方案。
-   在 Windows 8 和更高版本上测试 WDDM 1.0 和1.1 驱动程序。
-   尽快为 WDDM 1.2 驱动程序提供完整的零售包。

**独立软件供应商 (Isv) ：**

-   在 Windows 8 和更高版本上通过 WDDM 1.2 驱动程序测试现有和即将推出的 Microsoft DirectX 游戏。
-   在 Windows 8 和更高版本上测试单独的应用程序。
-   利用 Windows 8 DirectX 功能改进。

 

