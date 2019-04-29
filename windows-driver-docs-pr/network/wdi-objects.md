---
title: Wi-fi 设备模型和对象
description: 在两种类型的对象适配器和端口的上下文中的主机使用的 Wi-fi 设备。
ms.assetid: 0F375ED7-CB20-4F32-8ECE-4822D7787327
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6464ee4e0c5a2f7820382b710cd230b1a1caa990
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385324"
---
# <a name="wi-fi-device-model-and-objects"></a>Wi-fi 设备模型和对象


在两种类型的对象的上下文中的主机使用的 Wi-fi 设备： 适配器和端口。

![wdi 设备型号](images/wdi-object-model.png)

## <a name="adapter"></a>适配器


该适配器对象表示的 Wi-fi 设备中的 Wi-fi 功能。 命令和对此对象指示用于指示有关 Wi-fi 接口的状态。 对于具有多个 Wi-fi 设备的系统，每个适配器对象表示的另一个实例。

## <a name="port"></a>端口


可以是一个 Wi-fi 适配器同时使用多个连接例如基础结构客户端和 Wi-Fi Direct 组所有者。 Port 对象用于表示与每个此类连接关联的状态。 每个端口保存连接的 MAC 状态和任何物理状态特定于该连接。

适配器可以是多个端口。 在端口上发出的命令应该只会影响保留该端口的状态。

操作系统使用的操作模式，如 802.11 工作站、 Wi-Fi Direct 客户端或 Wi-Fi Direct 组所有者配置每个端口。 由操作模式和端口的状态确定固件必须准备好处理给定端口上的组命令。 一个端口可以采用两种状态之一：INIT 和 OP. 该端口是最初处于初始化状态且仅当操作系统发出一条命令 （如果客户端基础结构） 连接或启动亚太/转时将转换为操作状态。 端口返回到 init 函数运行时[OID\_WDI\_任务\_DOT11\_重置](https://msdn.microsoft.com/library/windows/hardware/dn925952)发送到 IHV 组件。

## <a name="port-availability-requirements"></a>端口可用性要求


| 端口类型                        | 所需的计数        |
|----------------------------------|-----------------------|
| 工作站端口                     | 1                     |
| Wi-Fi Direct 设备              | 1 （如果支持）      |
| Wi-Fi Direct 角色 （转到或客户端） | 1 或 2 （如果支持） |

 

## <a name="port-concurrency-requirements"></a>并发的端口要求


不同的端口类型的以下并发要求如下所示。

1.  1 个工作站端口都始终可用。
2.  1 个 Wi-Fi Direct 设备端口都始终可用。
3.  以下配置中提供了 2 个 Wi-Fi Direct 角色端口。
    1.  1 转
    2.  1 个客户端
    3.  转到 1，1 个客户端

 

 





