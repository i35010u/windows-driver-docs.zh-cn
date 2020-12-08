---
title: 无头系统支持
description: Windows 8 支持在没有任何图形硬件的情况下启动。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cea94a6356d2cab45f4d2bf77f42a4c62c3a97e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837783"
---
# <a name="support-for-headless-systems"></a>无头系统支持


Windows 8 支持在没有任何图形硬件的情况下启动。 如果未找到显示设备，则可以通过使用存根显示输出来完成此操作。 此存根显示将作为 (MSBDD) 的内置 Microsoft 基本显示器驱动程序的一部分实现。

由于在没有 PnP 驱动程序可用时使用存根显示，因此不需要第三方驱动程序。 它既适用于正常操作，也适用于系统崩溃，因此，无需硬件或固件支持即可伪造显示设备。

在检测到 VGA 的体系结构上，MSBDD 要求确认不存在 VGA;否则，会假设 VGA 硬件可用且系统不是无外设。 系统固件应在 FADT 的 IAPC 启动模式字段中设置 VGA Not in 标志 \_ \_ ，如果有任何 VBIOS，则应通过 VESA BIOS 扩展 (VBE) 来实现空模式列表。 这些机制应该表明即使系统实现了具有 int 10h 模式的 VBIOS，也不会出现 VGA，12小时支持与以前版本的 Windows 兼容。 在缺少 VBE 支持的情况下，基本显示器驱动程序使用由启动加载器初始化的显示，因此无外设系统不应通过 UEFI GOP 表示工作显示。

 

 





