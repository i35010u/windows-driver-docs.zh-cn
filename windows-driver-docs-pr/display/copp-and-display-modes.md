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
ms.openlocfilehash: ded167c890e83ac087cfddcdc2d5b3daa3365f2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839785"
---
# <a name="copp-and-display-modes"></a>COPP 和显示模式


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

无论当前使用何种显示模式，视频微型端口驱动程序都应报告与 DirectX VA COPP 设备关联的物理连接器支持的所有保护类型。 当视频微型端口驱动程序收到对其[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)函数的调用时，它会报告受支持的保护类型，并在 DXVA 的**guidStatusRequestID**成员中设置 DXVA\_COPPQueryProtectionType [ **\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)结构。 有关详细信息，请参阅[COPP Status](copp-status.md)。

如果对于特定保护类型，当前解决方法过高，则当调用视频微型端口驱动程序的[*COPPCommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数来为该保护类型设置保护级别时，驱动程序将返回错误。 以下方案举例说明了驱动程序的*COPPCommand*函数应何时返回 success 或错误：

-   如果 DirectX VA COPP 设备与 S-视频输出连接器相关联，则对视频微型端口驱动程序的[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)函数的调用 DXVA\_COPPQueryProtectionType 设置应指示支持模拟内容保护（ACP）type （COPP\_ProtectionType\_ACP）。 此后，如果调用驱动程序的[*COPPCommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数来为此连接器上的 ACP 类型设置级别，则驱动程序应返回 success，因为 s-视频的输出分辨率是固定的，即使桌面分辨率（显示模式）可能会更高。

-   如果 DirectX VA COPP 设备与组件输出连接器相关联，则对视频微型端口驱动程序的[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)函数的调用 DXVA\_COPPQueryProtectionType 设置还应指示 ACP 类型的支持。 但是，如果在显示分辨率为720p 或1080i 时调用驱动程序的[*COPPCommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数来为此输出设置 ACP 类型的级别，则驱动程序应返回 DDERR\_TOOBIGSIZE 错误代码，因为解决方法太高，无法设置组件输出连接器上 ACP 类型的保护级别。

 

 





