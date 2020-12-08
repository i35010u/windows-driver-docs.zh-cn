---
title: 注册辅助安装程序
description: 注册辅助安装程序
keywords:
- 共同安装程序 WDK 设备安装，注册
- 注册共同安装程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dee3a1f8d4042a9159d02dfe78ccfb70136edfca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815289"
---
# <a name="registering-a-co-installer"></a>注册辅助安装程序





可以为单个设备或特定安装程序类中的所有设备注册共同安装程序。 设备特定的共同安装程序会在安装其其中一个设备时通过 INF 文件进行动态注册。 类共同安装程序手动注册，或者由自定义设备安装应用程序和 INF 注册。

有关详细信息，请参阅

[注册特定于设备的辅助安装程序](registering-a-device-specific-co-installer.md)

[注册类辅助安装程序](registering-a-class-co-installer.md)

若要更新共同安装程序，DLL 的每个新版本都应有一个新文件名，因为当用户单击设备属性页上的 "更新驱动程序" 按钮时，DLL 通常正在使用中。

 

 





