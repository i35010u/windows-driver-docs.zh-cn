---
title: 处理保护级别
description: 处理保护级别
ms.assetid: d8237a48-9e1c-4b9e-8f55-70820ff08460
keywords:
- 复制保护 WDK COPP，保护级别
- 视频复制保护 WDK COPP，保护级别
- COPP WDK DirectX VA，保护级别
- 受保护视频 WDK COPP，保护级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 013d5be001e9f9b684cc66dc2803978b7a8f8a62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359320"
---
# <a name="handling-protection-levels"></a>处理保护级别


## <span id="ddk_handling_protection_levels_gg"></span><span id="DDK_HANDLING_PROTECTION_LEVELS_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

对于图形适配器支持保护的每个输出连接器，微型端口驱动程序应维护全局引用计数为每种保护类型和每个保护级别。 请注意，默认全局引用计数器被初始化为 0。

视频课程创建 DirectX VA COPP 设备后，COPP 设备应包含每个保护级别的每种保护类型的本地引用计数。 该驱动程序应为每个保护类型设置为值 1 和每个保护类型设置为值 0 的剩余保护级别计数器设置的默认保护级别计数器。

当视频会话将新的保护级别设置为特定的保护类型时，驱动程序应递减引用计数的当前保护级别，应增加新的保护级别的引用计数。 相应的更改也应该对全球引用级别计数器。

每当更改任何全局级别计数器时，驱动程序应检查特定输出连接器的所有计数器，并确保保护级别设置为对应于其值大于 0 的最高级别计数器的级别。 有关详细信息，请参阅中的示例代码[ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)并[ *COPPQueryStatus* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)参考页。

大于 0 的全局引用计数器时，微型端口驱动程序应将内容保护应用于输出 connector。 只要全局引用计数器达到 0，微型端口驱动程序应从输出连接器删除内容保护。 每当显示驱动程序接收到调用其[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)回调函数 (和视频的微型端口驱动程序接收到调用，反过来，其[ *COPPCloseVideoSession* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession)函数)，该视频的微型端口驱动程序应递减 COPP 设备的本地引用计数器的当前级别的全局引用计数器。 微型端口驱动程序只应从已认证的输出连接器删除内容保护，如果连接器的全局引用计数器达到 0。

**请注意**   *DdMoCompDestroy*可能调用函数，而 COPP 设备的本地引用计数器仍设置为大于 0 （例如，如果用户模式进程异常终止）。

 

 

 





