---
title: NFC 类扩展接口
description: NFC CX 接口基于 UMDF 类扩展模型。
ms.assetid: 400043BE-4C16-40C7-B0EB-BA223F882F21
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e2f43750a5b4527120003315007c58c7117283a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382505"
---
# <a name="nfc-class-extension-interface"></a>NFC 类扩展接口


NFC CX 接口基于 UMDF 类扩展模型。 NFC CX 接口允许 NFC 客户端将类实现卸载到 Microsoft 提供的类扩展，实现 NFC CX 接口，同时允许客户端驱动程序执行特定于传输的初始化和 i/o 处理，并充当 NFC 控制器所需的所有供应商特定功能的主机。

NFC CX 接口包括以下方法：

-   [**NfcCxDeviceInitConfig**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitconfig)
-   [**NfcCxDeviceInitialize**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)
-   [**NfcCxDeviceDeinitialize**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdevicedeinitialize)
-   [**NfcCxHardwareEvent**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxhardwareevent)
-   [**NfcCxNciReadNotification**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)
-   [**NfcCxSetRfDiscoveryConfig**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)
-   [**NfcCxSetLlcpConfig**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetllcpconfig)
-   [**NfcCxRegisterSequenceHandler**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxregistersequencehandler)
-   [**NfcCxUnRegisterSequenceHandler**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxunregistersequencehandler)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)