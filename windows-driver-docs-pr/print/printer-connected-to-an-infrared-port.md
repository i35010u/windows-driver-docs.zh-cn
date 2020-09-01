---
title: 连接到红外端口的打印机
description: 连接到红外端口的打印机
ms.assetid: 8545cf66-9b5c-41e8-82e0-e0edd75ad41b
keywords:
- 红外端口 WDK 打印机
- IR 端口 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71a8cfb937630ecc54d9e02b2586a6c93fa9b65e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207085"
---
# <a name="printer-connected-to-an-infrared-port"></a>连接到红外端口的打印机





通过红外 (IR) 端口连接的打印机不支持使用1284设备字符串的即插即用。 对于带有 IR 端口的计算机，服务会持续轮询设备。 当在范围内引入 IR 即插即用打印机时，将在 "枚举根" 下创建一个 PDO，其 \\ \\ *设备 ID* 格式为 "HWP*nnnn*"。 *Devnode*的*硬件 ID*包含一个 HWP*nnnn*格式的条目。

支持通过 LPT 和 IR 端口即插即用的打印机的 [**INF 制造商部分**](../install/inf-manufacturer-section.md) 条目应如下所示：

```cpp
 
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234, Model_Name_XYZ
"Model Name XYZ" = Install_Section_XYZ, HWP9876, Model_Name_XYZ
```

 

