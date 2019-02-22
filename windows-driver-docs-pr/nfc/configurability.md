---
title: 可配置性
description: 此主题 discuses 扩展性 NFC 客户端驱动程序，使客户端驱动程序配置许多其操作的参数将指向可用。
ms.assetid: 29C6C96E-9F20-4750-ABDD-103871B405FA
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63bdc7235c1291bd1fe2259585712197717af45d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555573"
---
# <a name="configurability"></a>可配置性


除了扩展点供 NFC 客户端驱动程序，NFC CX 还允许客户端驱动程序配置许多其操作的参数。 通过 NFC 客户端驱动程序，可以自定义以下配置。

-   驱动程序标志
-   RF 发现配置
-   LLCP 配置

## <a name="driver-flags"></a>驱动程序标志


NFC CX 允许 NFC 客户端驱动程序，以提供[**驱动程序标志**](https://msdn.microsoft.com/library/windows/hardware/dn905542)配置类扩展的运行时实现。 这些标志允许 NFC CX，若要实现某些标准 NCI 操作略有不同，由于不同的固件实现由于 NCI 规范中的多义性。

## <a name="rf-discovery-configuration"></a>RF 发现配置


可以将 RF 发现配置设置 NFC 客户端驱动程序通过[ **NfcCxSetRfDiscoveryConfig** ](https://msdn.microsoft.com/library/windows/hardware/dn905616)方法。 RF 发现配置应完成后调用的初始化期间[ **NfcCxDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905611)，否则返回错误。

## <a name="llcp-configuration"></a>LLCP 配置


可以将 LLCP 配置设置 NFC 客户端驱动程序通过[ **NfcCxSetLlcpConfig** ](https://msdn.microsoft.com/library/windows/hardware/dn905615) NFC CX 由提供的方法。 应在初始化后完成 LLCP configuration [ **NfcCxDeviceInitialize**](https://msdn.microsoft.com/library/windows/hardware/dn905611)，否则返回错误。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  
