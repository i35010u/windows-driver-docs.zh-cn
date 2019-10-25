---
title: 初始化序列
description: 下图说明了在初始化期间 NFC CX 和 NFCC 交换的一组高级 NCI 包。
ms.assetid: 4977E1D4-2546-4573-B555-FA87DB8A2168
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4433e99906369e310c978be4f9214d1ec023bbf4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838034"
---
# <a name="initialization-sequence"></a>初始化序列


下图说明了在初始化期间 NFC CX 和 NFCC 交换的一组高级 NCI 包。 在开始初始化之前，NFC CX 驱动程序会调用客户端驱动程序的预初始化序列处理程序（如果已注册）。 StateInit 包含以下高级序列： NCI reset、NCI 初始化、参数的标准 NCI 配置，以及 RF 接口和 RF 协议映射。 请注意，NFC 客户端驱动程序可以通过 NFC CX 接口功能（如[**NfcCxSetRfDiscoveryConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)和[**NfcCxSetLlcpConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxsetllcpconfig)）设置在初始化期间使用的某些 NCI 配置参数的默认值。 初始化完成后，将调用初始化完成序列处理程序。 完成初始化后的下一个状态为 StateRfIdle。

![初始化序列](images/initializationsequence.png)

正常运行 NFCC 的关键要求之一是处理 NFC 客户端驱动程序的固件下载操作。 NFC CX 设计的灵活性足以支持多种不同的设计，以便将固件下载到控制器。

某些芯片组要求 NCI 初始化固件版本信息，以确定是否需要下载固件。 对于此类设计，将显示用于完成固件下载的 NFC CX 和 NFC 客户端驱动程序的状态机，如下所示。 蓝色状态对应于 NFC CX 指定的状态，灰色状态对应于 NFC 客户端驱动程序中的状态。 Post NCI 初始化（即在初始化完成序列处理程序中），客户端驱动程序将从核心\_INIT\_RSP 消息检查当前版本，并确定是否需要固件下载操作。 如果为 "否"，则 NFC CX 驱动程序的正常状态转换将继续到下一个状态。 如果为 "是"，则客户端驱动程序请求 NFC CX 执行重启。 关闭后，NFC 客户端驱动程序可以实现固件下载。

![固件下载后初始化](images/initializationsequence1.png)

某些 NFCC 固件实现具有带外机制，即在 NCI 上下文之外，以确定是否需要下载固件。 在这种情况下，在处理预初始化序列时，NFC 客户端驱动程序可以实现其连接器状态，以确定是否需要下载固件。 如果为 "是"，则固件下载操作由客户端驱动程序执行。 如果为 "否"，则不需要固件下载，则会继续正常操作到下一个状态。 下图显示固件下载预 NCI 初始化的状态机处理。

![固件下载预初始化](images/firmwaredownloadpreinitialization.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

