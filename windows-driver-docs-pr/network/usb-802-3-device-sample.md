---
title: USB 802.3 设备示例
description: USB 802.3 设备示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 870e1c3af38d90aa554336b70975a1ca90f77c6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838718"
---
# <a name="usb-8023-device-sample"></a>USB 802.3 设备示例





下面是 USB 远程 NDIS 以太网设备的示例描述符集。 它包括 CDC 通信类接口和 CDC 数据类接口。 设备描述符是独立返回的。 配置描述符和所有以下描述符将作为单个块以显示的顺序返回。

控制消息是在控制终结点上发送的。 通知消息是在 CDC 通信类接口中的终结点上发送的。 数据消息是在 CDC 数据类接口中的批量传入和批量输出终结点上发送的。 不显示字符串说明符。

Windows Millennium Edition 中的远程 NDIS 实现假定通信类接口在数据类接口之前。 供应商应选择此描述符顺序，以便设备在 Windows Millennium Edition 上正确初始化。

如果此示例的任何部分与控制规范相矛盾，请遵循规范。

 

 





