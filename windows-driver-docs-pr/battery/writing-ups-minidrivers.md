---
title: 编写 UPS 微型驱动程序
description: 编写 UPS 微型驱动程序
ms.assetid: 85142cbf-cb3b-4ccf-a005-8fcb7a7ad12b
keywords:
- UPS 微型驱动程序 WDK
- 简单的信号 WDK
- 智能信号 WDK
- UPS 服务 WDK
- 系统提供 UPS 服务 WDK
- UPS 微型驱动程序 WDK，有关编写 UPS 微型驱动程序
- 不间断电源 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfa4cc4cd7f1cfef40ac34d4f5a3d5f5e3142679
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355240"
---
# <a name="writing-ups-minidrivers"></a>编写 UPS 微型驱动程序


## <span id="ddk_writing_ups_minidrivers_kg"></span><span id="DDK_WRITING_UPS_MINIDRIVERS_KG"></span>


如果不间断电源 (UPS) 连接到 Microsoft Windows 系统**UPS**选项卡上的**电源选项**控制面板中提供了有关 UPS 的信息。 在 Windows Server 2003、 Windows XP 和 Windows 2000 上，系统提供 UPS 服务连接到 COM 端口和该支持"简单信号，"可提供非常有限的控制功能和状态信息的 UPS 单元提供支持。

在 Windows Server 2003、 Windows XP 和 Windows 2000 上，如果 UPS 模型连接到的 COM 端口和支持"智能信号，"则应提供 UPS 微型驱动程序。 此微型驱动程序，这是用户模式 DLL 由系统的 UPS 服务调用，将执行以下操作：

-   初始化到 UPS 的通信路径。

-   更新注册表项的**电源选项**用于获得要显示的特定于模型的信息。

-   将根据请求 UPS 电源关闭。

-   监视状态更改的 UPS 单位。

UPS 微型驱动程序有关的详细信息，请参阅以下主题：

[UPS 微型驱动程序功能](ups-minidriver-functionality.md)

[UPS 注册表项](ups-registry-entries.md)

[示例 UPS 微型驱动程序](sample-ups-minidriver.md)

[安装 UPS 微型驱动程序](installing-ups-minidrivers.md)

**请注意**   Windows Vista 和更高版本的 Windows 不支持连接到 COM 端口的 UPS 单位。 这些 Windows 版本继续支持通过连接的 UPS 单位[USB](https://docs.microsoft.com/windows-hardware/drivers/)。

 

 

 




