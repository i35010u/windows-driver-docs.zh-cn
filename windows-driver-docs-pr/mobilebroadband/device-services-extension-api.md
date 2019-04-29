---
title: 设备服务扩展 API
description: 设备服务扩展 API
ms.assetid: e1539ae1-78fd-4d79-81bf-4030e69e191c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d31db3adff55b008392fcbf834a115b33026129
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380270"
---
# <a name="device-services-extension-api"></a>设备服务扩展 API


符合 Windows 的移动宽带设备项目用作设备服务的每个受支持的功能。 服务的示例包括 IP 连接 （连接到或从移动宽带网络断开连接的功能）、 通讯簿、 SIM 工具包、 SMS 和 USSD。 每个设备服务都有一个相应的 GUID。 所有控制消息和移动宽带通用驱动程序和设备携带 GUID 来标识与请求关联的服务之间交换的非 IP 数据包。 服务的 GUID 命名空间下定义的命令标识符 (Cid) 和状态指示代码。 例如，通讯簿和 SIM 工具包可能这两者共享相同的 CID 代码，但它们的区别的设备服务交换请求中的 GUID。

可以通过设备服务扩展 API 访问不由 Windows 无线平台本机实现的任何设备服务。 此 API 可直接访问设备上的独立硬件供应商 (IHV) 软件管道。 此管道提供的管道通过 WWAN 服务和移动宽带通用驱动程序到设备，如以下关系图中所示：

![设备服务](images/mb-fig1-deviceservices.png)

Windows 无线平台支持以下应用函数的 Api:

-   枚举设备的服务

-   打开/关闭设备服务

-   将控制命令发送到特定设备服务

-   将数据发送到 （或接收中的数据） 的一个特定的设备服务

-   注册"未经请求的"设备事件从特定设备服务

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的列表](list-of-mobile-broadband-windows-runtime-apis.md)

 

 






