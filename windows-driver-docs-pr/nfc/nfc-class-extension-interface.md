---
title: NFC 类扩展接口
description: NFC CX 接口基于 UMDF 类扩展模型。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a936b21ab5febb8c2f2154019b1901eeab48708
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813523"
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
