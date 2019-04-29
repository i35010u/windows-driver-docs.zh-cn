---
title: 连接到红外端口的打印机
description: 连接到红外端口的打印机
ms.assetid: 8545cf66-9b5c-41e8-82e0-e0edd75ad41b
keywords:
- 红外端口 WDK 打印机
- 红外端口 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14311a13add007c681bbf34f69c934f4162755a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354829"
---
# <a name="printer-connected-to-an-infrared-port"></a>连接到红外端口的打印机





通过红外线 (IR) 端口连接的打印机不支持使用 1284年设备字符串的插。 对于使用红外线 （ir） 端口的计算机，一个服务不断轮询的设备。 当 IR Plug and Play 打印机范围内，在枚举下面创建一个 PDO\\根\\与*设备 ID*窗体 HWP*nnnn*。 *硬件 ID*的*devnode*有单个条目的窗体 HWP*nnnn*。

[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)通过 LPT 和红外端口支持插的打印机的条目应显示如下所示：

```cpp
 
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234, Model_Name_XYZ
"Model Name XYZ" = Install_Section_XYZ, HWP9876, Model_Name_XYZ
```

 

 




