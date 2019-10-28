---
title: NFP 推动的外设无线设备配对
description: NFP 推动的外设无线设备配对
ms.assetid: 7B57019F-C80A-4E74-BBC2-A26BEDEB20DD
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70eda4791fc6abc95525372b6ffdcc9a87c419ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838883"
---
# <a name="nfp-facilitated-peripheral-wireless-device-pairing"></a>NFP 推动的外设无线设备配对


使用 NFP 技术可以实现的一个方案是将无线设备（如蓝牙键盘、鼠标和耳机）与 Windows 配对。 仅支持单向配对。 不支持智能设备（如手机）所需的双向配对。

为了实现这种配对，设备需要将其传输特定的配对信息提供给 NFP 技术。 对于蓝牙鼠标，鼠标将需要根据蓝牙 SIG 的定义发布标准的蓝牙带外（OOB）配对信息。 NFP 提供程序需要从设备读取 OOB 数据，并将其提交给为配对类型消息订阅的 Windows 服务。

NFP 提供程序必须了解并处理蓝牙配对类型消息。 它们由*messageType*参数的类型组件标识。 例如，"配对：蓝牙" 可能对应于支持静态蓝牙 OOB 配对的设备。 当 NFP 提供程序收到其中一条配对消息时，它必须将消息只转换为标准 OOB 配对数据，并删除任何特定于技术的协议信息（如 NDEF 标头）。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

