---
title: 内核模式性能监视
description: 内核模式性能监视
ms.assetid: 317d2f9d-db50-4513-8bbd-28f429236877
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1ba55fd7065e6e506f311b615c7f5b58925a4b6
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385081"
---
# <a name="kernel-mode-performance-monitoring"></a>内核模式性能监视

Microsoft Windows 操作系统允许系统组件和第三方使用 [性能计数器](/windows/win32/perfctrs/performance-counters-portal)以标准方式公开性能指标。

部分包括以下主题：

[关于内核模式性能计数器](about-kernel-mode-performance-counters.md)

[使用内核模式性能计数器](using-kernel-mode-performance-counters.md)

内核模式性能计数器使用以下 DDIs：

## <a name="kernel-mode-performance-counter-provider-functions"></a>内核模式性能计数器提供程序函数

[PcwAddInstance](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwaddinstance)

[PcwCallback](/windows-hardware/drivers/ddi/wdm/nc-wdm-pcw_callback)

[PcwCloseInstance](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwcloseinstance)

[PcwCreateInstance](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwcreateinstance)

[PcwRegister](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwregister)

[PcwUnregister](/windows-hardware/drivers/ddi/wdm/nf-wdm-pcwunregister)

## <a name="kernel-mode-performance-counter-structures-and-enumerations"></a>内核模式性能计数器结构和枚举

[PCW_CALLBACK_INFORMATION](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_callback_information)

[PCW_CALLBACK_TYPE](/windows-hardware/drivers/ddi/wdm/ne-wdm-_pcw_callback_type)

[PCW_COUNTER_DESCRIPTOR](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_descriptor)

[PCW_COUNTER_INFORMATION](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_information)

[PCW_DATA](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_counter_information)

[PCW_MASK_INFORMATION](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_mask_information)

[PCW_REGISTRATION_INFORMATION](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pcw_registration_information)