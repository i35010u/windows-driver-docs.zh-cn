---
title: NFC 类扩展体系结构
description: NFC 驱动程序作为类扩展实现，基础传输驱动程序作为客户端驱动程序实现。
ms.assetid: 9C68B3F7-CD83-4BDB-A4DD-11B7C1448301
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eb2a9caecccf06bf2c94907fb500514925364b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837738"
---
# <a name="nfc-class-extension-architecture"></a>NFC 类扩展体系结构


NFC 驱动程序作为类扩展实现，基础传输驱动程序作为客户端驱动程序实现。 整体驱动程序的主要优势是，将来可以将客户端传输驱动程序替换为支持其他传输，或为尚未通过 NFC 标准化的功能支持芯片制造商的特定需求讨论.

UMDF 2.0 中包含对类扩展的支持。 由于 NFC 堆栈不依赖于内核模式下提供的核心系统组件和受424Kbps 限制的技术的性能要求，因此此驱动程序没有理由在内核模式下运行。

| 文件          | 描述                                                                                                                                                                                                                                                                                                                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| NfcCx     | 此 DLL 包含 NFC 类驱动程序实现。 它依赖于 UMDF，并通过组件清单安装。 DLL 是符合核心系统的二进制文件，它与核心系统中提供的内容不具有任何依赖关系。 此 DLL 通过 NfcCxStub 库间接链接到客户端驱动程序，使客户端驱动程序能够将其加载并启动其初始化。 |
| NfcCxStub | 此文件是存根库，使客户端驱动程序能够在不直接链接到 NfcCx 的情况下执行到 NfcCx 的加载时链接。                                                                                                                                                                                                                                                     |

 

NFC 类扩展驱动程序不应在更新操作系统上下文中运行。 但是，驱动程序应在 Microsoft 制造 OS （MMOS）中运行，以执行行尾测试。 芯片组制造商提供的 NFC 客户端驱动程序可以针对制造和终结线测试目的实现额外的 DDI 支持，但这超出了本文档的范围。

 
 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

