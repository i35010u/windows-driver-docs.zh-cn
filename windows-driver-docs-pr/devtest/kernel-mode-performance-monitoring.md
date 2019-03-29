---
title: 内核模式性能监视
description: 内核模式性能监视
ms.assetid: 317d2f9d-db50-4513-8bbd-28f429236877
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09b71c8ab6452098ebe8a2012d23bb71641727d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575929"
---
# <a name="kernel-mode-performance-monitoring"></a>内核模式性能监视

Microsoft Windows 操作系统允许系统组件和第三方使用以标准方式公开性能指标[性能计数器](https://go.microsoft.com/fwlink/p/?linkid=144442)。

部分包括以下主题：

[内核模式下的性能计数器](about-kernel-mode-performance-counters.md)

[使用内核模式性能计数器](using-kernel-mode-performance-counters.md)

内核模式性能计数器将使用以下 DDIs:

## <a name="kernel-mode-performance-counter-provider-functions"></a>内核模式性能计数器提供程序功能

[PcwAddInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwaddinstance)

[PcwCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pcw_callback)

[PcwCloseInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwcloseinstance)

[PcwCreateInstance](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwcreateinstance)

[PcwRegister](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwregister)

[PcwUnregister](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pcwunregister)

## <a name="kernel-mode-performance-counter-structures-and-enumerations"></a>内核模式性能计数器结构和枚举

[PCW_CALLBACK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_callback_information)

[PCW_CALLBACK_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pcw_callback_type)

[PCW_COUNTER_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_counter_descriptor)

[PCW_COUNTER_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_counter_information)

[PCW_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_counter_information)

[PCW_MASK_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_mask_information)

[PCW_REGISTRATION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pcw_registration_information)
