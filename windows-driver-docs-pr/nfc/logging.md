---
title: 日志记录
ms.assetid: CB7FE988-6E5A-4669-9FFB-A2B3F8DAF30F
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: NFC 的函数/方法、 NCI 数据包/协议和其他详细日志记录的日志记录。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cf627fd102ebf04e36d01296e70efd718ecbeed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375111"
---
# <a name="logging"></a>日志记录


为函数/方法和其他详细日志记录， *Windows 软件跟踪预处理器*使用 (WPP) 日志记录。 对于 NCI 数据包/协议日志记录，使用事件跟踪 Windows (ETW)。 若要启用 WPP 调试日志记录，请使用以下命令：

```cpp
tracelog -start MyNfcSession -f C:\Data\test\bin\MyNfcSession.etl
tracelog -enableex MyNfcSession -guid #351734b9-8706-4cee-9247-04accd448c76 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #696D4914-12A4-422C-A09E-E7E0EB25806A -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #9d97cb90-8dee-42b8-b553-d1816be6fb9e -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #4EB7CC58-145C-4a79-9418-68CD290DD9D4 -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -enableex MyNfcSession -guid #D976D933-B88B-4227-95F8-00513C0986DE -matchanykw 0xFFFFFFFFFFFFFFFF -level 7
tracelog -stop MyNfcSession
```

这将生成一个名为 c： 驱动器中的 MySession.etl 的 ETL 文件\\数据文件夹。 你可以然后对其进行解码使用[Tracepdb](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracepdb) (Tracepdb.exe) 和[Tracefmt](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracefmt) (Tracefmt.exe)，Windows 驱动程序工具包中包括哪些。

NFC CX 不包括任何调试扩展。

## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC 类扩展 (CX) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[Windows （Windows 驱动程序） 的事件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-software-tracing)  
[用于软件跟踪的工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)  
