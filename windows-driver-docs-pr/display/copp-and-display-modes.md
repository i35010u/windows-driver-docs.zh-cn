---
title: COPP 和显示模式
description: COPP 和显示模式
ms.assetid: e7da753d-0ccd-428e-b51f-3fd0a19674e8
keywords:
- 复制保护 WDK COPP，显示模式
- 视频副本保护 WDK COPP，显示模式
- COPP WDK DirectX VA，显示模式
- 受保护的视频 WDK COPP，显示模式
- 显示模式 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd0f4a46d58e01ce6e83dff6d943615cf3a2560c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064894"
---
# <a name="copp-and-display-modes"></a>COPP 和显示模式


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

无论当前使用何种显示模式，视频微型端口驱动程序都应报告与 DirectX VA COPP 设备关联的物理连接器支持的所有保护类型。 当视频微型端口驱动程序收到对其[*COPPQueryStatus*](./coppquerystatus.md)函数的调用时，该驱动程序会报告支持的保护类型 \_ 。 [** \_ **](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput) **guidStatusRequestID** 有关详细信息，请参阅 [COPP Status](copp-status.md)。

如果对于特定保护类型，当前解决方法过高，则当调用视频微型端口驱动程序的 [*COPPCommand*](./coppcommand.md) 函数来为该保护类型设置保护级别时，驱动程序将返回错误。 以下方案举例说明了驱动程序的 *COPPCommand* 函数应何时返回 success 或错误：

-   如果 DirectX VA COPP 设备与 S-视频输出连接器相关联，则通过 DXVA COPPQueryProtectionType set 对视频微型端口驱动程序的 [*COPPQueryStatus*](./coppquerystatus.md) 函数进行调用时， \_ 应指出支持模拟内容保护 (ACP) 类型 (COPP \_ ProtectionType \_ ACP) 。 此后，如果调用驱动程序的 [*COPPCommand*](./coppcommand.md) 函数来为此连接器上的 ACP 类型设置级别，则驱动程序应返回成功，因为 s-视频的输出分辨率是固定的，即使桌面分辨率 (显示模式) 可能更高。

-   如果 DirectX VA COPP 设备与组件输出连接器相关联，则通过 DXVA COPPQueryProtectionType set 对视频微型端口驱动程序的 [*COPPQueryStatus*](./coppquerystatus.md) 函数进行调用时， \_ 还应指示 ACP 类型的支持。 但是，如果在显示分辨率为720p 或1080i 时调用驱动程序的 [*COPPCommand*](./coppcommand.md) 函数来为此输出设置 ACP 类型的级别，则驱动程序应返回 DDERR \_ TOOBIGSIZE 错误代码，因为该解决方法太高，无法设置组件输出连接器上 ACP 类型的保护级别。

 

