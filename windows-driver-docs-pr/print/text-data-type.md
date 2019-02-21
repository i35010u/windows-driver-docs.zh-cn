---
title: TEXT 数据类型
description: TEXT 数据类型
ms.assetid: 4d84b639-70e3-48e5-bfcc-61849e835710
keywords:
- 打印处理器 WDK，数据类型
- 数据类型 WDK 打印处理器
- TEXT 数据类型 WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd2ec92382c65390e6ca6ad7410410d38ba72562
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543564"
---
# <a name="text-data-type"></a>TEXT 数据类型





文本数据只包含 ANSI 文本。 打印处理器调用 GDI 绘制字符使用打印设备的默认字体，并将生成的原始格式输出发送到后台处理程序 (通过调用**WritePrinter**、 Microsoft Windows SDK 文档中所述)。 该过程等同于使用记事本打开输入的文件，然后打印该文件。 （此格式用于打印机无法打印文本字符。）

关于 TEXT 数据类型的详细信息，请参阅*Windows 2000 Professional Resource Kit*或*Windows 2000 Server Resource Kit*。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 




