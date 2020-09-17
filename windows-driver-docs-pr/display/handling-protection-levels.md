---
title: 处理保护级别
description: 处理保护级别
ms.assetid: d8237a48-9e1c-4b9e-8f55-70820ff08460
keywords:
- 复制保护 WDK COPP，保护级别
- 视频副本保护 WDK COPP，保护级别
- COPP WDK DirectX VA，保护级别
- 受保护的视频 WDK COPP，保护级别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa4142822239c5f28274d6f55090e617f92cdb62
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715324"
---
# <a name="handling-protection-levels"></a>处理保护级别


## <span id="ddk_handling_protection_levels_gg"></span><span id="DDK_HANDLING_PROTECTION_LEVELS_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

对于支持保护的图形适配器的每个输出连接器，视频微型端口驱动程序应为每个保护类型和每个保护级别维护全局引用计数。 请注意，默认全局引用计数器将初始化为0。

为视频会话创建 DirectX VA COPP 设备后，COPP 设备应在每个保护级别为每个保护类型包含本地引用计数。 驱动程序应将每个保护类型的默认保护级别计数器设置为值1，将每个保护类型的剩余保护级别计数器设置为值0。

当视频会话为特定保护类型设置新保护级别时，驱动程序应减小当前保护级别的引用计数，并应增加新保护级别的引用计数。 还应对全局引用级别计数器进行相应的更改。

任何全局级别计数器发生变化时，驱动程序都应检查特定输出连接器的所有计数器，并确保将保护级别设置为对应于值大于0的最高级别计数器的级别。 有关详细信息，请参阅 [*COPPCommand*](./coppcommand.md) 和 [*COPPQueryStatus*](./coppquerystatus.md) 参考页中的示例代码。

当全局引用计数器大于0时，视频微型端口驱动程序应将内容保护应用到输出连接器。 一旦全局引用计数器达到0，视频微型端口驱动程序就会删除输出连接器的内容保护。 只要显示驱动程序收到对其 [*DdMoCompDestroy*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 回调 (函数的调用，则视频微型端口驱动程序将收到对其 [*COPPCloseVideoSession*](./coppclosevideosession.md) 函数的调用) ，视频微型端口驱动程序应将全局引用计数器降低 COPP 设备的本地引用计数器的当前级别。 如果连接器的全局引用计数器达到0，则视频微型端口驱动程序应仅从认证的输出连接器中删除内容保护。

**注意**   当 COPP 设备的本地引用计数器仍设置为大于 0 (例如，如果用户模式进程异常终止) ，则可能会调用*DdMoCompDestroy*函数。

 

 

