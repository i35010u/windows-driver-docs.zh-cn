---
title: 内核模式性能监视
description: 内核模式性能监视
ms.assetid: 317d2f9d-db50-4513-8bbd-28f429236877
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447859191174145b0981b2ac2eb7a75b08b5258b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839544"
---
# <a name="kernel-mode-performance-monitoring"></a>内核模式性能监视

Microsoft Windows 操作系统允许系统组件和第三方使用[性能计数器](https://go.microsoft.com/fwlink/p/?linkid=144442)以标准方式公开性能指标。

部分包括以下主题：

[关于内核模式性能计数器](about-kernel-mode-performance-counters.md)

[使用内核模式性能计数器](using-kernel-mode-performance-counters.md)

内核模式性能计数器使用以下 DDIs：

## <a name="kernel-mode-performance-counter-provider-functions"></a>内核模式性能计数器提供程序函数

[PcwAddInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwaddinstance)

[PcwCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pcw_callback)

[PcwCloseInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwcloseinstance)

[PcwCreateInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwcreateinstance)

[PcwRegister](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)

[PcwUnregister](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)

## <a name="kernel-mode-performance-counter-structures-and-enumerations"></a>内核模式性能计数器结构和枚举

[PCW_CALLBACK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_callback_information)

[PCW_CALLBACK_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pcw_callback_type)

[PCW_COUNTER_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_descriptor)

[PCW_COUNTER_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_information)

[PCW_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_information)

[PCW_MASK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_mask_information)

[PCW_REGISTRATION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_registration_information)
