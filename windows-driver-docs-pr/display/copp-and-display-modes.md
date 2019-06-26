---
title: COPP 和显示模式
description: COPP 和显示模式
ms.assetid: e7da753d-0ccd-428e-b51f-3fd0a19674e8
keywords:
- 复制保护 WDK COPP 显示模式
- 视频复制保护 WDK COPP 显示模式
- COPP WDK DirectX va，因此显示模式
- 受保护视频 WDK COPP，显示模式
- 显示模式 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b438aa71b0ff24f5eb07683650114aa6337f5fcb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370275"
---
# <a name="copp-and-display-modes"></a>COPP 和显示模式


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

微型端口驱动程序应报告所有物理连接器支持的保护类型与 DirectX VA COPP 设备，而不考虑当前正在使用的显示模式相关联。 微型端口驱动程序报告支持的保护类型，当它收到对的调用其[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)函数和 DXVA\_COPPQueryProtectionType 集中**guidStatusRequestID**的成员[ **DXVA\_COPPStatusInput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppstatusinput)结构。 有关详细信息，请参阅[COPP 状态](copp-status.md)。

如果当前的分辨率太高对于特定的保护类型，然后当微型端口驱动程序[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数调用以将保护级别设置为该保护类型，驱动程序应返回一个错误。 以下方案提供情形的示例驱动程序的*COPPCommand*函数应返回成功或错误：

-   如果 DirectX VA COPP 设备与 S-视频输出接口，微型端口驱动程序的调用相关联[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)函数和 DXVA\_COPPQueryProtectionType 设置应指示模拟内容保护 (ACP) 类型的支持 (COPP\_ProtectionType\_ACP)。 此后，如果驱动程序的[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)函数调用设置一个级别的 ACP 类型的此连接器，则驱动程序应返回成功，因为固定的 S-视频输出分辨率，甚至尽管桌面分辨率 （显示模式） 可能会更高版本。

-   DirectX VA COPP 设备是否与组件输出连接器，微型端口驱动程序的调用相关联[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)函数和 DXVA\_COPPQueryProtectionType 设置此外应该指示 ACP 类型的支持。 但是，如果驱动程序的[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)调用函数时显示分辨率为 720p 或 1080i ACP 类型在此输出上设置级别，则驱动程序应返回 DDERR\_TOOBIGSIZE 错误代码，因为的解决方法是过高，设置保护级别的 ACP 类型的组件输出连接器。

 

 





