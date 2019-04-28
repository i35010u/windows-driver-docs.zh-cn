---
title: 执行硬件功能性扫描
description: 执行硬件功能性扫描
ms.assetid: 966b30b7-2f08-4611-9f4d-f85b301de414
keywords:
- OPM WDK 显示 HFS
- OPM WDK 显示，硬件功能扫描
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4118d3b34858c9e4f86c8c2e5e2003e665faab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352314"
---
# <a name="performing-a-hardware-functionality-scan"></a>执行硬件功能性扫描


显示微型端口驱动程序的硬件功能扫描 (HFS) 可确保与所需的硬件进行通信的微型端口驱动程序。 有关 HFS 的详细信息，请下载处的输出内容保护文档[输出内容保护和 Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc)网站。

显示微型端口驱动程序必须启动执行 HFS 每当 Microsoft DirectX 图形内核子系统 (*Dxgkrnl.sys*) 调用以下驱动程序函数：

-   [**DxgkDdiStartDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   [**DxgkDdiSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_set_power_state)与图形适配器的电源状态设置为 D0。

HFS 可以是异步的并且不需要完成，然后才能[ **DxgkDdiStartDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)或[ **DxgkDdiSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_set_power_state)返回。 但是，没有[OPM DDI](supporting-output-protection-manager.md)函数可以返回到 HFS 完成时为止。
