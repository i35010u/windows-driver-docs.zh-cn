---
title: 编写 UPS 微型驱动程序
description: 编写 UPS 微型驱动程序
ms.assetid: 85142cbf-cb3b-4ccf-a005-8fcb7a7ad12b
keywords:
- UPS 微型驱动程序 WDK
- 简单的信号 WDK
- 智能信号 WDK
- UPS 服务 WDK
- 系统提供的 UPS 服务 WDK
- 有关微型驱动程序的信息，请阅读微型驱动程序
- 不间断电源 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d085a24ff19904e17bbf65528a8ca9b70ce7a013
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056869"
---
# <a name="writing-ups-minidrivers"></a>编写 UPS 微型驱动程序


## <span id="ddk_writing_ups_minidrivers_kg"></span><span id="DDK_WRITING_UPS_MINIDRIVERS_KG"></span>


如果连接到 Microsoft Windows 系统的不间断电源 (UPS) ，"控制面板" 中 "**电源选项**" 的 " **ups** " 选项卡提供有关 UPS 的信息。 在 Windows Server 2003、Windows XP 和 Windows 2000 上，系统提供的 UPS 服务提供对连接到 COM 端口并支持 "简单信号" （提供非常有限的控制功能和状态信息）的 UPS 单元的支持。

在 Windows Server 2003、Windows XP 和 Windows 2000 上，如果 UPS 型号连接到 COM 端口并支持 "智能信号"，则应提供 UPS 微型驱动程序。 此微型驱动程序是由系统的 UPS 服务调用的用户模式 DLL，它执行以下操作：

-   初始化对 UPS 的通信路径。

-   更新 **电源选项** 用于获取要显示的特定于模型的信息的注册表项。

-   关闭请求时的 UPS 电源。

-   监视 UPS 单元的状态更改。

有关 UPS 微型驱动程序的详细信息，请参阅以下主题：

[UPS 微型驱动程序功能](ups-minidriver-functionality.md)

[UPS 注册表项](ups-registry-entries.md)

[示例 UPS 微型驱动程序](sample-ups-minidriver.md)

[安装 UPS 微型驱动程序](installing-ups-minidrivers.md)

**注意**   Windows Vista 和更高版本的 Windows 不支持连接到 COM 端口的 UPS 设备。 这些 Windows 版本继续支持通过 [USB](../index.yml)连接的 UPS 设备。

 

 

