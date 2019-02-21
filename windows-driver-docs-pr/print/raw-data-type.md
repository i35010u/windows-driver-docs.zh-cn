---
title: 原始数据类型
description: 原始数据类型
ms.assetid: f53264c1-97aa-42f0-8bab-76bf984f2c79
keywords:
- 打印处理器 WDK，数据类型
- 数据类型 WDK 打印处理器
- 原始数据类型 WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06427b130d4960d932e6b992292d599243b84d30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540780"
---
# <a name="raw-data-type"></a>原始数据类型





原始数据可以发送到打印监视器中，而无需进一步处理。 打印处理器只需将此数据发送回后台处理程序 (通过调用**WritePrinter**、 Microsoft Windows SDK 文档中所述)，有时插入窗体馈送。 原始数据文件的一个示例是一个组成*打印机控制语言 (PCL)* 命令。 打印作业会从客户端到服务器以原始格式如果客户端或服务器不支持 NT 基于操作系统系统 EMF，或服务器管理员已禁用 EMF 支持。 在这种情况下，图像呈现作业发送到服务器之前在客户端上执行。

Postscript 命令能被视为原始数据，则目标打印机支持 Postscript。 另一方面，Sfmpsprt.dll 打印处理器所采取的 Postscript 输入，并将其解释为非 Postscript 的打印机，因此在这种情况下 Postscript 不是原始数据。

有关原始数据类型的详细信息，请参阅*Windows 2000 Professional Resource Kit*或*Windows 2000 Server Resource Kit*。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 




