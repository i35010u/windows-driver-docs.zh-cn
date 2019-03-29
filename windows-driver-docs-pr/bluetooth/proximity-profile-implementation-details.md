---
title: 邻近感应配置文件实现详细信息
description: 若要实现节能的设计，设备实现必须遵守特定的要求，以确保它们保持与 Windows 兼容。
ms.assetid: 0FFDF345-EA14-4564-AA8A-7E44E9DB28DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff3e69acee25b32c106caf504137d3cf78f52af2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568122"
---
# <a name="proximity-profile-implementation-details"></a>邻近感应配置文件实现详细信息


若要实现节能的设计，设备实现必须遵守特定的要求，以确保它们保持与 Windows 兼容。

以下子主题检查设备端要求来启用高效使用电源，以及描述一种技术可以依据监视连接状态。

## <a name="span-idestablishingaconnectionspanspan-idestablishingaconnectionspanspan-idestablishingaconnectionspanestablishing-a-connection"></a><span id="Establishing_a_Connection"></span><span id="establishing_a_connection"></span><span id="ESTABLISHING_A_CONNECTION"></span>建立连接


Windows 8.1 将自动连接到设备时应用程序已注册 GattCharacteristic.ValueChanged 事件的处理程序。 但是在邻近配置文件中包含的服务的基本定义不包含任何 indicatable 或可通知特征。 设备可以添加包含到邻近配置文件中包含的服务的 indicatable 或可通知特征的服务。 这意味着邻近设备必须支持至少一个 indicatable 或可通知的特性值，应用程序必须注册到自动建立连接的 GattCharacteristic.ValueChanged 事件至少一个处理程序。

## <a name="span-iddetectinglossofconnectionspanspan-iddetectinglossofconnectionspanspan-iddetectinglossofconnectionspandetecting-loss-of-connection"></a><span id="Detecting_Loss_of_Connection"></span><span id="detecting_loss_of_connection"></span><span id="DETECTING_LOSS_OF_CONNECTION"></span>检测连接的中断


如中所述[蓝牙近距离](bluetooth-proximity-profile.md)，Windows 8.1 不公开的蓝牙连接 RSSI 值。 因此，应用不能使用 RSSI 值来计算连接路径丢失。 相反，我们建议在设备绑定到链接的丢失事件与其附近。

## <a name="span-idmonitoringtheconnectionstatespanspan-idmonitoringtheconnectionstatespanspan-idmonitoringtheconnectionstatespanmonitoring-the-connection-state"></a><span id="Monitoring_the_connection_state"></span><span id="monitoring_the_connection_state"></span><span id="MONITORING_THE_CONNECTION_STATE"></span>监视连接状态


应用可以使用 PnpObjectWatcher 监视 GATT 设备的连接状态和监视服务的设备对象的即插即用"连接"属性。 此方法进行了演示[蓝牙泛型属性配置文件-心率服务](https://go.microsoft.com/fwlink/p/?linkid=301978)示例。

 

 





