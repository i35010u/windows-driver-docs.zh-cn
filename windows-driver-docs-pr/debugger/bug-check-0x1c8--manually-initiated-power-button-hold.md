---
title: Bug 检查 0x1C8 MANUALLY_INITIATED_POWER_BUTTON_HOLD
description: MANUALLY_INITIATED_POWER_BUTTON_HOLD bug 检查的值为0x000001CE。 系统已配置为在用户按住电源按钮时启动错误检测。
keywords:
- Bug 检查 0x1C8 MANUALLY_INITIATED_POWER_BUTTON_HOLD
- MANUALLY_INITIATED_POWER_BUTTON_HOLD
ms.date: 03/05/2021
topic_type:
- apiref
api_name:
- MANUALLY_INITIATED_POWER_BUTTON_HOLD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 15b25a074b666b6de8137b95eae3b01f81eca96b
ms.sourcegitcommit: 47cd14eb928aee3a3368d9d1d92a7047b30eac55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/11/2021
ms.locfileid: "103022570"
---
# <a name="bug-check-0x1c8-manually_initiated_power_button_hold"></a>Bug 检查0x1C8：手动 \_ 启动的 \_ 电源 \_ 按钮 \_ 挂起

手动 \_ 启动的 \_ 电源 \_ 按钮 \_ 保留值为0x000001C8。

系统已配置为当用户在指定的时间段保持电源按钮时启动错误检测。  这是一种诊断检测错误，用于在系统要在长时间按钮保持的情况下进行硬重置时捕获转储。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

请注意，当发生此 bug 检查而不是显示标准的 "蓝屏" 时，将显示带有以下文本的黑色背景，并显示% 完成指示器：

"请释放电源按钮。 只需几秒钟即可关闭。 "

## <a name="manually_initiated_power_button_hold-parameters"></a>手动 \_ 启动的 \_ 电源 \_ 按钮 \_ 保留参数

以下参数显示在蓝色屏幕上。

参数 | 描述
|---------|--------------|
1 | 按住电源按钮的时间（毫秒）。
2 | 指向 nt！ _POP_POWER_BUTTON_TRIAGE_BLOCK 的指针。
3 | 保留。
4 | 保留。

## <a name="see-also"></a>另请参阅

[使用电源按钮强制系统崩溃](forcing-a-system-crash-with-the-power-button.md)

[内部显示错误 0x1C8 MANUALLY_INITIATED_POWER_BUTTON_HOLD](https://channel9.msdn.com/Shows/Inside/0x1C8)

[ACPI 按钮设备](/windows-hardware/drivers/hid/acpi-button-device)
