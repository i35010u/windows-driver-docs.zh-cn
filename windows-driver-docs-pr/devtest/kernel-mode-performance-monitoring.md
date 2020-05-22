---
title: 内核模式性能监视
description: 内核模式性能监视
ms.assetid: 317d2f9d-db50-4513-8bbd-28f429236877
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7517d8f8c437a7189f61471c4074db209f8e02f
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769427"
---
# <a name="kernel-mode-performance-monitoring"></a>内核模式性能监视

Microsoft Windows 操作系统允许系统组件和第三方使用[性能计数器](https://docs.microsoft.com/windows/win32/perfctrs/performance-counters-portal)以标准方式公开性能指标。

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
