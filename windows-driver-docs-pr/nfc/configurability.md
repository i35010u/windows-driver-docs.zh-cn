---
title: 可配置性
description: 本主题 discuses 可用于 NFC 客户端驱动程序的扩展点，使客户端驱动程序可以配置其多个操作的参数。
ms.assetid: 29C6C96E-9F20-4750-ABDD-103871B405FA
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5be86a42d07ddbca4e2a3a755ead62003d31f038
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843430"
---
# <a name="configurability"></a>可配置性


除了可用于 NFC 客户端驱动程序的扩展点之外，NFC CX 还允许客户端驱动程序配置其多个操作的参数。 NFC 客户端驱动程序可以自定义以下配置。

-   驱动程序标志
-   RF 发现配置
-   LLCP 配置

## <a name="driver-flags"></a>驱动程序标志


NFC CX 允许 NFC 客户端驱动程序提供[**驱动程序标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/ne-nfccx-_nfc_cx_driver_flags)来配置类扩展的运行时实现。 这些标志允许 NFC CX 实现某些标准 NCI 操作的方式略有不同，因为 NCI 规范中的歧义导致了不同的固件实现。

## <a name="rf-discovery-configuration"></a>RF 发现配置


通过[**NfcCxSetRfDiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)方法，NFC 客户端驱动程序可以设置 RF 发现配置。 RF 发现配置应在调用[**NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)之后的初始化过程中完成，否则返回错误。

## <a name="llcp-configuration"></a>LLCP 配置


NFC 客户端驱动程序可以通过 NFC CX 提供的[**NfcCxSetLlcpConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetllcpconfig)方法设置 LLCP 配置。 LLCP 配置应在[**NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)之后的初始化过程中完成，否则返回错误。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
