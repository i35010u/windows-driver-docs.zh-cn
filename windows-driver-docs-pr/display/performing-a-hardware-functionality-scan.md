---
title: 执行硬件功能性扫描
description: 执行硬件功能性扫描
ms.assetid: 966b30b7-2f08-4611-9f4d-f85b301de414
keywords:
- OPM WDK 显示，HFS
- OPM WDK 显示，硬件功能扫描
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ae9161cf8188579fb61a047a11f01cd6498587a
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066462"
---
# <a name="performing-a-hardware-functionality-scan"></a>执行硬件功能性扫描


显示微型端口驱动程序的硬件功能扫描 (HFS) 确保微型端口驱动程序与所需的硬件通信。 有关 HFS 的详细信息，请在 [输出内容保护和 Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc) 网站上下载内容保护文档的输出。

每当 Microsoft DirectX 图形内核子系统 (*Dxgkrnl.sys*) 调用以下驱动程序函数时，显示微型端口驱动程序必须开始执行 HFS：

-   [**DxgkDdiStartDevice**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   将图形适配器的电源状态设置为 "D0" 的[**DxgkDdiSetPowerState**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state) 。

HFS 可以是异步的，并且不需要在 [**DxgkDdiStartDevice**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device) 或 [**DxgkDdiSetPowerState**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state) 返回之前完成。 但是，在 HFS 完成之前，不会返回 [OPM DDI](supporting-output-protection-manager.md) 函数。