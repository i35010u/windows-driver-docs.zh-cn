---
title: NFP 推动的外设无线设备配对
description: NFP 推动的外设无线设备配对
ms.assetid: 7B57019F-C80A-4E74-BBC2-A26BEDEB20DD
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88935187221e5e387936a63f7dd6cc4b31e75fb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378641"
---
# <a name="nfp-facilitated-peripheral-wireless-device-pairing"></a>NFP 推动的外设无线设备配对


NFP 技术如何帮助的方案之一是与 Windows 的蓝牙键盘、 鼠标和耳机等的无线设备配对。 支持仅单向配对。 不支持双向配对智能手机等设备所需的。

若要完成这种配对，设备需要 NFP 技术提供其特定于传输的配对信息。 在蓝牙鼠标的情况下鼠标将需要定义蓝牙签名的发布标准蓝牙带外 (OOB) 配对的信息， NFP 提供程序需要从设备读取该 OOB 数据并将其传送到订阅配对类型的消息的 Windows 服务。

NFP 提供程序必须理解和处理蓝牙配对类型的消息。 这些标识的类型组件*messageType*参数。 一个示例可能是"配对： 蓝牙"，它们会分别对应于支持静态蓝牙 OOB 配对的设备。 当 NFP 提供程序收到其中一种配对消息时，它必须将该消息转换到只需标准 OOB 配对的数据，删除任何特定于技术的协议信息 （如 NDEF 标头）。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

