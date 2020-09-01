---
title: Wi-fi 设备型号和对象
description: Wi-fi 设备由主机在两种类型的对象适配器和端口的上下文中使用。
ms.assetid: 0F375ED7-CB20-4F32-8ECE-4822D7787327
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ade25e6c54e9c4e95e78e11f929d7224287edc4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216824"
---
# <a name="wi-fi-device-model-and-objects"></a>Wi-fi 设备型号和对象


Wi-fi 设备由主机在两种类型的对象的上下文中使用：适配器和端口。

![wdi 设备型号](images/wdi-object-model.png)

## <a name="adapter"></a>适配器


适配器对象表示 Wi-fi 设备中的 Wi-fi 功能。 此对象上的命令和指示用于指示有关 Wi-fi 接口的状态。 对于具有多个 Wi-fi 设备的系统，每个适配器对象表示不同的实例。

## <a name="port"></a>端口


一个 Wi-fi 适配器可以同时用于多个连接，例如，基础结构客户端和 Wi-fi Direct 组所有者。 Port 对象用于表示与每个此类连接相关联的状态。 每个端口都具有连接的 MAC 状态以及特定于该连接的任何 phy 状态。

适配器中可以有多个端口。 端口上发出的命令只会影响为该端口维护的状态。

操作系统使用操作模式配置每个端口，例如802.11 工作站、Wi-fi Direct Client 或 Wi-fi Direct 组所有者。 固件必须准备好在给定端口上处理的设置命令由操作模式和端口状态决定。 端口可以处于以下两种状态之一： INIT 和 OP。 此端口最初处于初始状态，并且仅当操作系统发出命令以连接 (时，才会转换为操作状态，这种情况下，基础结构客户端) 或启动 AP/中转。 当 [OID \_ WDI \_ TASK \_ DOT11 \_ RESET](./oid-wdi-task-dot11-reset.md) 发送到 IHV 组件时，该端口返回到 INIT 状态。

## <a name="port-availability-requirements"></a>端口可用性要求


| 端口类型                        | 所需计数        |
|----------------------------------|-----------------------|
| 工作站端口                     | 1                     |
| Wi-fi Direct 设备              | 1 (（如果支持）)       |
| Wi-fi Direct 角色 (中转或客户端)  | 1或 2 (（如果支持）)  |

 

## <a name="port-concurrency-requirements"></a>端口并发要求


不同端口类型的以下并发要求如下所示。

1.  1个工作站端口始终可用。
2.  1 wi-fi Direct 设备端口始终可用。
3.  2 wi-fi 直接角色端口在以下配置中提供。
    1.  1开始
    2.  1个客户端
    3.  1开始，1个客户端

 

