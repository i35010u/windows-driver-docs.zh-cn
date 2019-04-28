---
title: /Debug 开关
description: /Debug 转换来增强存储证书管理工具的报告的功能，并在 IEEE 1667 合规 USB 存储设备中存储有关身份验证接收器证书 (ASC) 的信息。
ms.assetid: 9a7c8fd0-34a8-4f60-a8cb-d5777645f672
keywords:
- / 调试开关驱动程序开发工具
topic_type:
- apiref
api_name:
- /Debug
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea6712be11ed34a234460ee6088d2b81c349a40d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344013"
---
# <a name="debug-switch"></a>/Debug 开关


/**调试**开关的增强存储证书管理工具的报告功能和 IEEE 1667 合规的 USB 存储设备中的身份验证接收器证书 (ASC) 存储有关的信息。 此报告包括以下几个部分：

-   用于哈希和签名算法。

-   证书槽的总数。

-   已占用和空证书槽数。

**请注意**在本主题中，指定的 IEEE 1667 合规 USB 存储设备称为*目标设备*。



```
    EhStorCertMgrCmd /Debug -Volume:
    VolumeName
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-卷：**   
目标设备的卷名称。 此参数的格式的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**请注意**若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，输入**EhStorCertMgrCmd /List**从命令行。



### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例显示了从生成的输出的摘录 **/debug**切换：

```
Execute Debug operation for specified volume name...

Certificate silo device Capabilities...

Certificate Extension Parsing :- 1
Render User Data Unusable :- 1

Hash Algorithm :-
1.3.14.3.2.26
2.16.840.1.101.3.4.2.1
2.16.840.1.101.3.4.2.2
2.16.840.1.101.3.4.2.3

Asymmetric Key Cryptography :-
1.2.840.113549.1.1.1,1024
1.2.840.113549.1.1.1,2048
1.2.840.113549.1.1.1,3072

Signing Algorithm :-
1.2.840.113549.1.1.10,1.3.14.3.2.26
1.2.840.113549.1.1.10,2.16.840.1.101.3.4.2.1
1.2.840.113549.1.1.10,2.16.840.1.101.3.4.2.2
1.2.840.113549.1.1.10,2.16.840.1.101.3.4.2.3
1.3.14.3.2.29
1.2.840.113549.1.1.5
1.2.840.113549.1.1.11
1.2.840.113549.1.1.12
1.2.840.113549.1.1.13

Firmware version :- 1.1

Specification version :- 1.1

Total available slots   :- 16
Occupied slots          :- 3
Free slots              :- 13
```





