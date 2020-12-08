---
title: WMI 体系结构
description: WMI 体系结构
keywords:
- WMI WDK 内核，体系结构
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ae8a9652510fce2c1e39508381d2d01c266000a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782697"
---
# <a name="wmi-architecture"></a>WMI 体系结构





为了支持 WMI，驱动程序将注册为 WMI 提供程序。 WMI 提供程序是一个 Win32 动态链接库 (DLL) ，用于处理 WMI 请求并提供 WMI 检测数据。 请参阅 [注册为 Wmi 数据提供程序](registering-as-a-wmi-data-provider.md) ，了解如何将驱动程序注册为 wmi 提供程序。

将驱动程序注册为 WMI 提供程序后，WMI 使用者会请求数据或调用由提供程序公开的方法。

查询请求从用户模式使用者向下传递到 WMI 内核模式服务，后者又将 IRP 请求发送到您的驱动程序。

例如，当 WMI 客户端请求给定的数据块时，WMI 内核组件会向该驱动程序发送查询请求，以检索或设置数据。 驱动程序处理 wmi 请求，如 [处理 Wmi 请求](handling-wmi-requests.md)中所述。

下图显示了此数据流：

![阐释 wmi 体系结构数据流的图示](images/wmi1a.png)

 

 




