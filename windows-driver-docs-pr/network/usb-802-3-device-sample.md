---
title: USB 802.3 设备示例
description: USB 802.3 设备示例
ms.assetid: 647dd493-a7f4-469a-ab2f-f58f9916333d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 117bbb3b51f40664a27c3b2580f679c82a299a5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380145"
---
# <a name="usb-8023-device-sample"></a>USB 802.3 设备示例





下面是示例集的描述符的 USB 远程 NDIS 以太网设备。 它包括 CDC 通信类接口和 CDC 数据类接口。 设备描述符是单独返回。 作为单个块中所示的顺序返回配置描述符和以下的所有描述符。

控制终结点发送控制消息。 在 CDC 通信类接口中的中断在终结点发送通知消息。 数据发送消息大容量中和大容量 Out 终结点中的 CDC 数据类接口。 不显示字符串描述符。

Windows Millennium Edition 中的远程 NDIS 实现假定通信类接口之前数据类接口。 供应商应选择排序，以便设备在 Windows Millennium Edition 上正确初始化此说明符。

如果此示例的任何部分不符合控制规范，请按照该规范。

 

 





