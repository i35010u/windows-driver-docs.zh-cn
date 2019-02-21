---
title: WDDM 1.2 最佳实践
description: 为了提供最佳体验在 Windows 8 和更高版本，Windows 会利用图形硬件与 Windows 显示器驱动程序模型 (WDDM) 1.2 或更高版本驱动程序配对。 本部分汇总了最佳实践。
ms.assetid: 130C66F0-1ACE-4C6E-AE16-AEFCD4847312
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5779f57d3a346fd6cb0e0c9df562cea5c769d75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541571"
---
# <a name="wddm-12-best-practices"></a>WDDM 1.2 最佳实践


为了提供最佳体验在 Windows 8 和更高版本，Windows 会利用图形硬件与 Windows 显示器驱动程序模型 (WDDM) 1.2 或更高版本驱动程序配对。 本部分汇总了最佳实践。

**系统制造商：**

-   请确保在以下情况下全面测试，十分适用于您的系统配置：
    -   与 Microsoft 基本显示驱动程序兼容
    -   不需要重新启动的服务器上的更新
-   设计与 WDDM 硬件的新服务器，采用最适合你的客户的需求的相关 WDDM 驱动程序类型。
-   使用图形硬件供应商以获取认证的 WDDM 1.2 驱动程序以进行验证。
-   对于无头系统：
    -   系统固件应设置 VGA 不存在标志中 IAPC\_启动\_体系结构字段的固定 ACPI 描述表 (FADT)，并且如果没有任何 VBIOS，它应实现通过 VESA BIOS 扩展 (VBE) 的空模式列表。
    -   如果没有 VBE 支持，无头系统不应表示工作显示通过统一可扩展固件接口 (UEFI) 的图形输出协议 (GOP)。
-   请参阅[Windows 硬件认证](https://go.microsoft.com/fwlink/p/?linkid=325510)进行验证和测试的信息。
-   测试不同的硬件配置上桌面和移动系统，以确保稳定的最终用户体验 Windows 8 及更高版本。

**图形硬件供应商：**

-   使用 Microsoft 开发了 WDDM 1.2 驱动程序。
-   测试预发行版 WDDM 1.2 驱动程序在 Windows 8 和更高版本。
-   向 Microsoft 提供更新的 WDDM 1.x 驱动程序通过 Windows 更新进行部署。
-   除了 Windows 认证测试套件中，验证图形和游戏性能、 应用程序兼容性，并在每个 ASIC 系列上的各种自承载方案。
-   测试 WDDM 1.0 和 1.1 驱动程序在 Windows 8 和更高版本。
-   提供完整的零售包 WDDM 1.2 驱动程序的最早。

**独立软件供应商 (Isv):**

-   测试与 WDDM 1.2 驱动程序在 Windows 8 和更高版本的现有和即将推出 Microsoft DirectX 游戏。
-   测试单个应用程序在 Windows 8 和更高版本。
-   充分利用 Windows 8 DirectX 功能改进。

 

 





