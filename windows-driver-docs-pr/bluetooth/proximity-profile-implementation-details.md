---
title: 邻近感应配置文件实现详细信息
description: 若要实现节能设计，设备实现必须遵循特定要求，以确保它们与 Windows 保持兼容。
ms.assetid: 0FFDF345-EA14-4564-AA8A-7E44E9DB28DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82b92e9c6297a18f6cb6ecf780e4bcbc38af658f
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733535"
---
# <a name="proximity-profile-implementation-details"></a>邻近感应配置文件实现详细信息


若要实现节能设计，设备实现必须遵循特定要求，以确保它们与 Windows 保持兼容。

以下子主题检查设备端要求以有效地使用电源，并描述可用于监视连接状态的技术。

## <a name="span-idestablishing_a_connectionspanspan-idestablishing_a_connectionspanspan-idestablishing_a_connectionspanestablishing-a-connection"></a><span id="Establishing_a_Connection"></span><span id="establishing_a_connection"></span><span id="ESTABLISHING_A_CONNECTION"></span>建立连接


当应用程序 GattCharacteristic 事件的处理程序已注册时，Windows 8.1 将自动连接到该设备。 但是，近程配置文件中包含的服务的基本定义不包含任何 indicatable 或可通知特性。 设备可以将包含 indicatable 或可通知特性的服务添加到邻近感应配置文件中包含的服务。 这意味着，近程设备必须至少支持一个 indicatable 或可通知特性值，并且应用程序必须将至少一个处理程序注册到 ValueChanged 事件，才能自动建立连接。

## <a name="span-iddetecting_loss_of_connectionspanspan-iddetecting_loss_of_connectionspanspan-iddetecting_loss_of_connectionspandetecting-loss-of-connection"></a><span id="Detecting_Loss_of_Connection"></span><span id="detecting_loss_of_connection"></span><span id="DETECTING_LOSS_OF_CONNECTION"></span>检测中断连接


如 [蓝牙邻近配置文件](bluetooth-proximity-profile.md)中所述，Windows 8.1 不会公开蓝牙连接的 RSSI 值。 因此，应用无法使用 RSSI 值来计算连接路径丢失。 相反，我们建议将设备连接到链接丢失事件的距离。

## <a name="span-idmonitoring_the_connection_statespanspan-idmonitoring_the_connection_statespanspan-idmonitoring_the_connection_statespanmonitoring-the-connection-state"></a><span id="Monitoring_the_connection_state"></span><span id="monitoring_the_connection_state"></span><span id="MONITORING_THE_CONNECTION_STATE"></span>监视连接状态


应用可以使用 PnpObjectWatcher 监视 GATT 设备的连接状态，并监视服务设备对象的 PnP "已连接" 属性。 [蓝牙一般属性配置文件-心率服务](/samples/browse/)示例中演示了此技术。

 

