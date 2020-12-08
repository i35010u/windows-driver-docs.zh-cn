---
title: 编写设备安装应用程序
description: 编写设备安装应用程序
keywords:
- 安装应用程序 WDK，有关编写安装应用程序的信息
- 设备安装应用程序 WDK，有关编写安装应用程序的信息
- 设备设置 WDK 设备安装，编写安装应用程序
- 安装设备 WDK，编写安装应用程序
- 编写设备安装应用程序
- 安装应用程序 WDK
- 设备安装应用程序 WDK
- 应用程序 WDK 设备安装
- 设备安装 WDK，应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53209dbc16dee58c63df717a3bf0945b3b8bfaee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840929"
---
# <a name="writing-a-device-installation-application"></a>编写设备安装应用程序





**注意**  通用或移动驱动程序包不支持本部分中介绍的功能。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 
如果驱动程序包中包含的驱动程序和 INF 文件替代了 "收件箱" 驱动程序和 INF 文件，或者包中包含设备特定的应用程序，则它应包含安装这些组件的 *设备安装应用程序* 。 设备安装应用程序和分发媒体应该与自动运行兼容，因此当用户插入分发媒体时，自动运行自动启动应用程序。 有关自动运行的详细信息，请参阅 [创建 AutoRun-Enabled 应用程序](/previous-versions/windows/desktop/legacy/cc144206(v=vs.85))。

有关如何编写设备安装应用程序的指南，请参阅 [编写设备安装应用程序的指南](guidelines-for-writing-device-installation-applications.md)。

[驱动程序包](driver-packages.md)必须处理两种情况：

1.  用户在插入分发媒体之前插入到你的硬件中。 这通常称为 [硬件第一次安装](hardware-first-installation.md)。

2.  用户在插入你的硬件之前插入你的分发媒介。 这通常称为 [软件优先安装](software-first-installation.md)。

 

