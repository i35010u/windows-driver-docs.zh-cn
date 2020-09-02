---
title: 日志记录
ms.assetid: CB7FE988-6E5A-4669-9FFB-A2B3F8DAF30F
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 用于函数/方法、NCI 数据包/协议和其他详细日志记录的 NFC 日志记录。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68efc52ff6164aef73781979d600edef0ac017bf
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382545"
---
# <a name="logging"></a>日志记录


对于函数/方法和其他详细日志记录，使用 *Windows 软件跟踪预处理器* (WPP) 日志记录。 对于 NCI 数据包/协议日志记录，使用 Windows (ETW) 的事件跟踪。 若要启用 WPP 日志记录以进行调试，请使用以下命令：

```cpp
tracelog -start MyNfcSession -f C:\Data\test\bin\MyNfcSession.etl
tracelog -enableex MyNfcSession -guid #351734b9-8706-4cee-9247-04accd448c76 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #696D4914-12A4-422C-A09E-E7E0EB25806A -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #9d97cb90-8dee-42b8-b553-d1816be6fb9e -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #4EB7CC58-145C-4a79-9418-68CD290DD9D4 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #D976D933-B88B-4227-95F8-00513C0986DE -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -stop MyNfcSession
```

这将在 C： Data 文件夹中生成一个名为 MySession 的 ETL 文件。 \\ 然后，你可以使用 [Tracepdb](../devtest/tracepdb.md) （包含在 Windows 驱动程序工具包中） ( # A0) 和 [Tracefmt](../devtest/tracefmt.md) ( # A1) 对其进行解码。

NFC CX 不包括任何调试扩展。

## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)  
[Windows (Windows 驱动程序的事件跟踪) ](../devtest/tools-for-software-tracing.md)  
[用于软件跟踪的工具](../devtest/wpp-software-tracing.md)