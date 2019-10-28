---
title: NFC 类扩展接口
description: NFC CX 接口基于 UMDF 类扩展模型。
ms.assetid: 400043BE-4C16-40C7-B0EB-BA223F882F21
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66b4a2152320e0111fb113e732d596c3c884640a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837750"
---
# <a name="nfc-class-extension-interface"></a>NFC 类扩展接口


NFC CX 接口基于 UMDF 类扩展模型。 NFC CX 接口允许 NFC 客户端将类实现卸载到 Microsoft 提供的类扩展，实现 NFC CX 接口，同时允许客户端驱动程序执行特定于传输的初始化和 i/o 处理，如并充当 NFC 控制器所需的所有供应商特定功能的主机。

NFC CX 接口包括以下方法：

-   [**NfcCxDeviceInitConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitconfig)
-   [**NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)
-   [**NfcCxDeviceDeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdevicedeinitialize)
-   [**NfcCxHardwareEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxhardwareevent)
-   [**NfcCxNciReadNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)
-   [**NfcCxSetRfDiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)
-   [**NfcCxSetLlcpConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetllcpconfig)
-   [**NfcCxRegisterSequenceHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxregistersequencehandler)
-   [**NfcCxUnRegisterSequenceHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxunregistersequencehandler)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

