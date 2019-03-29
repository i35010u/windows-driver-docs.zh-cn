---
title: 初始化序列
description: 下图演示了在初始化期间交换的 NFC CX 和 NFCC NCI 数据包高级组。
ms.assetid: 4977E1D4-2546-4573-B555-FA87DB8A2168
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df285c0593424bd4a1d41f6ea8c52d3595be99a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575384"
---
# <a name="initialization-sequence"></a>初始化序列


下图演示了在初始化期间交换的 NFC CX 和 NFCC NCI 数据包高级组。 在初始化开始时之前, NFC CX 驱动程序调用客户端驱动程序的初始化前序列处理程序，如果已注册了一个。 StateInit 包括以下高级序列：NCI 重置，NCI 初始化、 标准 NCI 配置参数和 RF 接口和 RF 协议映射。 请注意，NFC 客户端驱动程序可以设置一些如通过 NFC CX 界面函数的初始化期间使用的 NCI 配置参数的默认值[ **NfcCxSetRfDiscoveryConfig** ](https://msdn.microsoft.com/library/windows/hardware/dn905616)并[**NfcCxSetLlcpConfig**](https://msdn.microsoft.com/library/windows/hardware/dn905615)。 在初始化完成时，将调用 initialize 完整序列处理程序。 初始化完成后下, 一步的状态是 StateRfIdle。

![初始化序列](images/initializationsequence.png)

NFCC 正常的主要要求之一处理来自 NFC 客户端驱动程序的固件下载操作。 NFC CX 设计非常灵活，可以下载到控制器的固件支持多个不同的设计。

某些芯片集需要有关固件版本控制信息以确定是否需要固件下载 NCI 初始化。 对于此类设计用于完成固件下载 NFC CX 和 NFC 客户端驱动程序的状态机将出现如下所示。 蓝色状态对应于指定的 NFC CX 的状态和灰色状态对应于 NFC 客户端驱动程序中的状态。 在初始化完成序列处理程序，客户端驱动程序即 NCI 初始化后检查核心中的当前版本\_INIT\_RSP 消息，并确定是否需要固件下载操作。 如果否正常状态转换的 NFC CX 驱动程序将继续到下一步的状态。 如果是客户端驱动程序请求 NFC CX 执行重启。 关闭完成后，NFC 客户端驱动程序可以实现固件下载。

![固件下载后初始化](images/initializationsequence1.png)

某些 NFCC 固件实现包含带外机制，即外部的 NCI，以确定是否需要固件下载的上下文。 在这种情况下，处理预初始化序列时，NFC 客户端驱动程序可以实现其连接器状态，以确定是否需要固件下载。 如果是然后固件下载操作由执行客户端驱动程序。 如果否即固件下载不是必需的然后继续到下一个状态的正常操作。 下图显示了状态机的固件下载 Pre-NCI 初始化处理。

![固件下载预初始化](images/firmwaredownloadpreinitialization.png)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

