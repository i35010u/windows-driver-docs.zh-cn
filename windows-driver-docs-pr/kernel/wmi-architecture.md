---
title: WMI 体系结构
description: WMI 体系结构
ms.assetid: cdc8f318-1931-426e-bd9c-da7aa6a11036
keywords:
- WMI WDK 内核，体系结构
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78d025215e6de0ee64f6c527ed476df32696e5e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555881"
---
# <a name="wmi-architecture"></a>WMI 体系结构





若要支持 WMI，您的驱动程序将注册为 WMI 提供程序。 WMI 提供程序是的 Win32 动态链接库 (DLL) 处理 WMI 请求并提供 WMI 检测数据。 请参阅[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)若要了解如何将驱动程序注册为 WMI 提供程序。

您的驱动程序注册为 WMI 提供程序后，WMI 使用者则请求数据或调用由提供程序公开的方法。

从用户模式下的 WMI 内核模式服务，又将 IRP 请求发送到您的驱动程序的使用者的查询请求行程事件。

例如，当 WMI 客户端请求时给定的数据块，WMI 内核组件会将查询请求发送到驱动程序检索或设置数据。 该驱动程序处理 WMI 请求中所述[处理 WMI 请求](handling-wmi-requests.md)。

下图显示了此数据流：

![说明 wmi 体系结构数据流关系图](images/wmi1a.png)

 

 




