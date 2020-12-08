---
title: 连接到红外端口的打印机
description: 连接到红外端口的打印机
keywords:
- 红外端口 WDK 打印机
- IR 端口 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 869ed9481fbf13ba99e992e43fc0afbea3c71f5b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807337"
---
# <a name="printer-connected-to-an-infrared-port"></a>连接到红外端口的打印机





通过红外 (IR) 端口连接的打印机不支持使用1284设备字符串的即插即用。 对于带有 IR 端口的计算机，服务会持续轮询设备。 当在范围内引入 IR 即插即用打印机时，将在 "枚举根" 下创建一个 PDO，其 \\ \\ *设备 ID* 格式为 "HWP *nnnn*"。 *Devnode* 的 *硬件 ID* 包含一个 HWP *nnnn* 格式的条目。

支持通过 LPT 和 IR 端口即插即用的打印机的 [**INF 制造商部分**](../install/inf-manufacturer-section.md) 条目应如下所示：

```cpp
 
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234, Model_Name_XYZ
"Model Name XYZ" = Install_Section_XYZ, HWP9876, Model_Name_XYZ
```

 

