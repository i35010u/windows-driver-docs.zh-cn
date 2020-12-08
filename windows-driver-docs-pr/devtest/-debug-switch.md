---
title: /Debug 开关
description: 增强的存储证书管理工具的/Debug 交换机会报告有关身份验证接收器证书的功能和信息， (ASC) 存储在符合 IEEE 1667 的 USB 存储设备中。
keywords:
- /Debug 交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Debug
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5df1494d12739281de85e2448f14259f17f2d41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833573"
---
# <a name="debug-switch"></a>/Debug 开关


增强的存储证书管理工具的/**调试** 开关报告有关身份验证接收器证书的功能和信息， (ASC) 存储在符合 IEEE 1667 的 USB 存储设备中。 此报告包括以下部分：

-   用于哈希和签名的算法。

-   证书槽的总数。

-   已占用和空证书槽的数目。

**注意**  在本主题中，指定的与 IEEE 1667 兼容的 USB 存储设备称为 *目标设备*。



```
    EhStorCertMgrCmd /Debug -Volume:
    VolumeName
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span>**-Volume：**   
目标设备的卷名。 有关此参数的格式的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令行中输入 **EhStorCertMgrCmd/list** 。



### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例显示了 **/debug** 开关生成的输出的摘录：

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





