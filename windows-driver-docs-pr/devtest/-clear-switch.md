---
title: /Clear 开关
description: /Clear 开关指定 IEEE 1667 合规 USB 存储设备存储的证书的身份验证接收器证书 (ASC) 的大多数增强存储证书管理工具中删除。注意在本主题中，指定 IEEE 1667 合规 USB 存储设备被称为目标设备。
ms.assetid: b8002d0c-450a-4c4c-bee6-83e382984b34
keywords:
- / 清除交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Clear
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3217f60cad90fa6cc70e59d4489ef405fabad662
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344003"
---
# <a name="clear-switch"></a>/Clear 开关


**/Clear**增强存储证书管理工具的开关指定 IEEE 1667 合规 USB 存储设备上的身份验证接收器证书 (ASC) 存储中删除大部分的证书。

**请注意**在本主题中，指定的 IEEE 1667 合规 USB 存储设备称为*目标设备*。



```
    EhStorCertMgrCmd /Clear  -Volume:
    VolumeName
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume______"></span><span id="_______-volume______"></span><span id="_______-VOLUME______"></span> **-Volume**   
目标设备的卷名称。 此参数的格式的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**请注意**若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，请键入**EhStorCertMgrCmd /List**在命令提示符，然后按 Enter。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/Clear**交换机清除所有证书从目标设备，除了以下证书：

-   预配证书 (PCp)。 若要删除的 PCp 证书，必须使用[ **/Initialize 交换机**](-initialize-switch.md)。

-   ASC 制造商证书 (ASCm) 中。

    **请注意**的增强存储证书管理工具不能添加、 删除或替换从目标设备中的 ASC 存储区的 ASC 制造商 (ASCm) 证书。



要清除从目标设备的证书，设备必须具有已预配使用 PCp 证书，并且该证书的私钥必须驻留在主机，以与设备一起传递管理身份验证。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何清除从目标设备的证书：

```
EhStorCertMgrCmd /Clear -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```





