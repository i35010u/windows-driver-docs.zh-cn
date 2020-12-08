---
title: Wi-Fi 设备型号和对象
description: 主机在两个对象适配器和端口类型的上下文中由主机使用 Wi-Fi 设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6de1d37e2cc0cfda2e35f8e6c0bcfa9c47973a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807995"
---
# <a name="wi-fi-device-model-and-objects"></a>Wi-Fi 设备型号和对象


主机在两种类型的对象的上下文中使用 Wi-Fi 设备：适配器和端口。

![wdi 设备型号](images/wdi-object-model.png)

## <a name="adapter"></a>适配器


适配器对象表示 Wi-Fi 设备中的 Wi-Fi 功能。 此对象上的命令和指示用于指示有关 Wi-Fi 接口的状态。 对于具有多个 Wi-Fi 设备的系统，每个适配器对象表示不同的实例。

## <a name="port"></a>端口


一个 Wi-Fi 适配器可以同时用于多个连接，例如，基础结构客户端和 Wi-Fi 直属组所有者。 Port 对象用于表示与每个此类连接相关联的状态。 每个端口都具有连接的 MAC 状态以及特定于该连接的任何 phy 状态。

适配器中可以有多个端口。 端口上发出的命令只会影响为该端口维护的状态。

操作系统使用操作模式配置每个端口，例如802.11 工作站、Wi-Fi 直接客户端或 Wi-Fi 直属组所有者。 固件必须准备好在给定端口上处理的设置命令由操作模式和端口状态决定。 端口可以处于以下两种状态之一： INIT 和 OP。 此端口最初处于初始状态，并且仅当操作系统发出命令以连接 (时，才会转换为操作状态，这种情况下，基础结构客户端) 或启动 AP/中转。 当 [OID \_ WDI \_ TASK \_ DOT11 \_ RESET](./oid-wdi-task-dot11-reset.md) 发送到 IHV 组件时，该端口返回到 INIT 状态。

## <a name="port-availability-requirements"></a>端口可用性要求


| 端口类型                        | 所需计数        |
|----------------------------------|-----------------------|
| 工作站端口                     | 1                     |
| Wi-Fi 直接设备              | 1 (（如果支持）)       |
| Wi-Fi 直接角色 ("开始" 或 "客户端)  | 1或 2 (（如果支持）)  |

 

## <a name="port-concurrency-requirements"></a>端口并发要求


不同端口类型的以下并发要求如下所示。

1.  1个工作站端口始终可用。
2.  1 Wi-Fi 直接设备端口始终可用。
3.  2 Wi-Fi 在以下配置中提供直接角色端口。
    1.  1开始
    2.  1个客户端
    3.  1开始，1个客户端

 

