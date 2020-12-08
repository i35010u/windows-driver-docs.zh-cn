---
title: 设备服务扩展 API
description: 设备服务扩展 API
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1b193c3b5853072234b248aa6531376a59b1f26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788555"
---
# <a name="device-services-extension-api"></a>设备服务扩展 API


兼容 Windows 的移动宽带设备将每个受支持的功能投影为一个设备服务。 服务的示例有 (连接到移动宽带网络或从移动宽带网络断开连接或断开连接的能力) 、电话簿、SIM 工具包、SMS 和 USSD。 每个设备服务都有相应的 GUID。 在移动宽带通用驱动程序与设备之间交换的所有控制消息和非 IP 数据包都具有 GUID 来标识与请求关联的服务。 命令标识符 (Cid) 并且状态指示代码在服务的 GUID 命名空间下定义。 例如，电话簿和 SIM 工具包都可能共享相同的 CID 代码，但它们可以通过在请求中交换的设备服务 GUID 来区分。

由 Windows 无线平台本机实现的任何设备服务都可以通过设备服务扩展 API 进行访问。 此 API 为独立硬件供应商 (IHV) 软件提供直接管道来访问设备上的功能。 此管道通过 WWAN 服务和移动宽带通用驱动程序向设备提供管道，如下图所示：

![设备服务](images/mb-fig1-deviceservices.png)

Windows 无线平台支持适用于以下应用功能的 Api：

-   枚举设备服务

-   打开/关闭设备服务

-   向特定设备服务发送控制命令

-   将数据发送到 (或接收来自特定设备服务) 的数据

-   注册特定设备服务中的 "未经授权" 设备事件

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的列表](list-of-mobile-broadband-windows-runtime-apis.md)

 

 






