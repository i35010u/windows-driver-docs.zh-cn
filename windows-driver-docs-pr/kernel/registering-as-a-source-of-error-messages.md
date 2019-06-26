---
title: 注册为错误消息的源
description: 注册为错误消息的源
ms.assetid: 5428950c-9c28-411a-9ec0-b029ad311a00
keywords:
- 源注册 WDK 错误
- 错误 WDK 内核
- 注册错误消息源
- 注册表 WDK 错误日志
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec9724a0588d10dae007381b30eb38aa85aa4458
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373477"
---
# <a name="registering-as-a-source-of-error-messages"></a>注册为错误消息的源





驱动程序在注册表中注册错误消息的源。 驱动程序必须设置两个密钥下的**HKEY\_本地\_机\\系统\\CurrentControlSet\\Services\\EventLog\\系统\\** <em>DriverName</em>:

<a href="" id="eventmessagefile--reg-expand-sz-"></a>**EventMessageFile** (REG\_EXPAND\_SZ)  
错误消息源之间用分号分隔的列表。 如果驱动程序使用标准错误类型，此列表必须包含 iologmsg.dll。 如果驱动程序将使用附加到驱动程序映像的错误消息，这必须包括驱动程序映像的名称。

<a href="" id="typessupported--reg-dword-"></a>**TypesSupported** (REG\_DWORD)  
可以记录可能的严重级别的位掩码。 驱动程序通常将此项设置为 7，以指示它们可能会记录所有严重级别。

有关如何将驱动程序的 INF 文件中设置这些注册表项的说明，请参阅[**注册事件日志记录**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)。

 

 




