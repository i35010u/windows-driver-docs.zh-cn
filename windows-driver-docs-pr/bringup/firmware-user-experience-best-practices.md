---
title: 固件用户体验 (UX) 最佳做法
description: 固件用户体验 (UX) 最佳做法
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: b9999b902b1793370c76ebdce2fabb4107cab063
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187647"
---
# <a name="firmware-user-experience-ux-best-practices"></a>固件用户体验 (UX) 最佳做法


系统的固件更新对于该计算机的持续使用非常重要。 Microsoft 希望确保固件更新安全传送，并且安装不会中断。 为此，我们建议你在 " **相关资源** " 部分中更详细地介绍了以下准则。

1.  进度栏/指示系统正在安装更新。

2.  使用 **UpdateCapsule** 函数的 Windows 启动加载程序将为用户提供包含消息的位图。

3.  UEFI 检查 AC 电源，或者电池使用充足 (RSOC) 还是出现故障，并在 ESRT 中记录错误代码。

**相关资源**链接包含有关固件 UX 指导的最新信息。

## <a name="related-resources"></a>相关资源

[Windows UEFI 固件更新平台](./windows-uefi-firmware-update-platform.md)

[无缝危机预防和恢复](./seamless-crisis-prevention-and-recovery.md)

[UEFI 固件更新的用户体验](./user-experience-for-uefi-firmware-updates.md)

[启动屏幕组件](./boot-screen-components.md)

[ESRT 表定义](./esrt-table-definition.md)

[验证 Windows UEFI 固件更新平台功能](/windows-hardware/manufacture/desktop/validating-windows-uefi-firmware-update-platform-functionality)