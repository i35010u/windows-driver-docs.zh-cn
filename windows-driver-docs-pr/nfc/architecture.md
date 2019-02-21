---
title: NFC 类扩展体系结构
description: 作为类扩展实现 NFC 驱动程序和基础传输驱动程序作为客户端驱动程序。
ms.assetid: 9C68B3F7-CD83-4BDB-A4DD-11B7C1448301
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bedaaf2c5fec499b87672ea0d39171aa210cdffb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543335"
---
# <a name="nfc-class-extension-architecture"></a>NFC 类扩展体系结构


作为类扩展实现 NFC 驱动程序和基础传输驱动程序作为客户端驱动程序。 通过单一式驱动程序的主要优点是，客户端传输驱动程序替换为在将来以支持其他传输或尚未标准化通过 NFC 的功能支持的芯片制造商的特定需求论坛。

UMDF 2.0 中包含的类扩展的支持。 NFC 堆栈在内核模式和权限隐含的一种技术，以 424 kbps 速率进行限制的性能要求中可用的核心的系统组件不有任何依赖项，因为内核模式中对函数的此驱动程序的理由。

| 文件          | 描述                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| NfcCx.dll     | 此 DLL 包含 NFC 类驱动程序实现。 它在 UMDF 上具有依赖关系并安装通过组件清单。 DLL 是一项核心系统符合二进制没有上述任何依赖什么是核心系统中提供。 DLL 间接链接到客户端驱动程序通过 NfcCxStub 库，可以使用客户端驱动程序，以将其加载并启动其初始化。 |
| NfcCxStub.lib | 此文件是客户端驱动程序可执行加载时链接到 NfcCx.dll 不直接将链接到 NfcCx.lib 的存根 （stub） 库。                                                                                                                                                                                                                                                     |

 

NFC 类扩展驱动程序不应在更新 OS 上下文中运行。 但是，该驱动程序应运行在 Microsoft 生产 OS (MMO) 执行行尾测试。 芯片组制造商提供的 NFC 客户端驱动程序可以实现其他 DDI 支持用于制造和行结束测试目的，但这超出了本文档的范围。

 
 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

