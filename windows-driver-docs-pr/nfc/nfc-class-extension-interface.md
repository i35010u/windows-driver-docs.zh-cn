---
title: NFC 类扩展接口
description: NFC CX 界面基于 UMDF 类扩展模型。
ms.assetid: 400043BE-4C16-40C7-B0EB-BA223F882F21
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60d7e74f98e30aa4ff0f22085b1be7ddff40ca5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543750"
---
# <a name="nfc-class-extension-interface"></a>NFC 类扩展接口


NFC CX 界面基于 UMDF 类扩展模型。 NFC CX 界面允许 NFC 客户端将卸载到实现 NFC CX 界面，同时允许客户端驱动程序中要执行特定于传输的初始化和 I/O 处理，Microsoft 提供的类扩展的类实现也可充当主机上的 NFC 控制器所需的所有特定于供应商的功能。

NFC CX 界面包括以下方法：

-   [**NfcCxDeviceInitConfig**](https://msdn.microsoft.com/library/windows/hardware/dn905610)
-   [**NfcCxDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905611)
-   [**NfcCxDeviceDeinitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905609)
-   [**NfcCxHardwareEvent**](https://msdn.microsoft.com/library/windows/hardware/dn905612)
-   [**NfcCxNciReadNotification**](https://msdn.microsoft.com/library/windows/hardware/dn905613)
-   [**NfcCxSetRfDiscoveryConfig**](https://msdn.microsoft.com/library/windows/hardware/dn905616)
-   [**NfcCxSetLlcpConfig**](https://msdn.microsoft.com/library/windows/hardware/dn905615)
-   [**NfcCxRegisterSequenceHandler**](https://msdn.microsoft.com/library/windows/hardware/dn905614)
-   [**NfcCxUnRegisterSequenceHandler**](https://msdn.microsoft.com/library/windows/hardware/dn905617)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

