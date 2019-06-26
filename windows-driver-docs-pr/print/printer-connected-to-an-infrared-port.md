---
title: 连接到红外端口的打印机
description: 连接到红外端口的打印机
ms.assetid: 8545cf66-9b5c-41e8-82e0-e0edd75ad41b
keywords:
- 红外端口 WDK 打印机
- 红外端口 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8fa5091cdaafcf25f28b685ce69ead29318a0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380665"
---
# <a name="printer-connected-to-an-infrared-port"></a>连接到红外端口的打印机





通过红外线 (IR) 端口连接的打印机不支持使用 1284年设备字符串的插。 对于使用红外线 （ir） 端口的计算机，一个服务不断轮询的设备。 当 IR Plug and Play 打印机范围内，在枚举下面创建一个 PDO\\根\\与*设备 ID*窗体 HWP*nnnn*。 *硬件 ID*的*devnode*有单个条目的窗体 HWP*nnnn*。

[ **INF 制造商部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)通过 LPT 和红外端口支持插的打印机的条目应显示如下所示：

```cpp
 
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234, Model_Name_XYZ
"Model Name XYZ" = Install_Section_XYZ, HWP9876, Model_Name_XYZ
```

 

 




