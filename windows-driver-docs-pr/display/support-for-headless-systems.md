---
title: 无头系统的提供支持
description: Windows 8 支持启动而无需任何图形硬件。
ms.assetid: 6351F6F9-6666-4040-A82A-3813ACCE8DEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 522b2b4c9efc7792de9edc840d69f9c0a7bd09b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543865"
---
# <a name="support-for-headless-systems"></a>无头系统的提供支持


Windows 8 支持启动而无需任何图形硬件。 使用存根 （stub） 显示输出，如果没有显示设备找不到完成此操作。 此存根 （stub） 显示作为部件的现成 Microsoft 基本显示驱动程序 (MSBDD) 实现。

由于没有即插即用驱动程序可用时使用的存根 （stub） 显示，则没有第三方驱动程序是必需的。 它适用于这两个正常的操作和出现的系统损坏，因此需要以伪显示设备不的任何硬件或固件支持。

在其中 VGA 已被一种规范的体系结构上, MSBDD 需要 VGA 不存在; 的肯定确认否则，它假定 VGA 硬件可用，并且系统不是无外设。 系统固件应设置 VGA 不存在标志中 IAPC\_启动\_FADT 的体系结构字段，如果没有任何 VBIOS，它应实现通过 VESA BIOS 扩展 (VBE) 的空模式列表。 这些机制应指示 VGA 不存在即使系统实现 VBIOS int 10 h 模式 12 小时支持与以前版本的 Windows 兼容性。 如果没有 VBE 支持，基本显示驱动程序使用初始化的引导加载程序，因此无头系统不应表示通过 UEFI GOP 工作显示的显示。

 

 





