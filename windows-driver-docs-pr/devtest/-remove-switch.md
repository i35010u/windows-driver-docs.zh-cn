---
title: /Remove 开关
description: 增强型存储证书管理工具的 /Remove 开关从身份验证接收器证书 (ASC) 存储在 IEEE 1667 合规 USB 存储设备中删除指定的证书。请注意到生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表、 命令提示符下键入 EhStorCertMgrCmd /List，然后按 Enter。
ms.assetid: c74fe7c3-264e-4bbd-9036-b5a254b3ba5b
keywords:
- / 删除交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Remove
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fed0152a0c2205763ab058072da62f7162b4758
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361723"
---
# <a name="remove-switch"></a>/Remove 开关


**/Remove**增强存储证书管理工具的开关从身份验证接收器证书 (ASC) 存储在 IEEE 1667 合规 USB 存储设备中删除指定的证书。

**请注意**若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，请键入**EhStorCertMgrCmd /List**在命令提示符，然后按 Enter。



```
    EhStorCertMgrCmd /Remove  -Volume:
    VolumeName
     -Index:
    IndexValue
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-卷：**   
目标设备的卷名称。 此参数的格式的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**请注意**若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，请键入**EhStorCertMgrCmd /List**在命令提示符，然后按 Enter。



<span id="_______-Index_______"></span><span id="_______-index_______"></span><span id="_______-INDEX_______"></span> **-索引：**   
其中将删除该证书的 ASC 存储区中的索引。 索引值必须大于 1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/Remove**开关从以下证书除目标设备中删除所有的证书：

-   预配证书 (PCp)。 若要删除的 PCp 证书，必须使用[ **/Initialize 交换机**](-initialize-switch.md)。

-   ASC 制造商证书 (ASCm) 中。

    **请注意**的增强存储证书管理工具不能添加、 删除或替换从目标设备中的 ASC 存储区的 ASC 制造商 (ASCm) 证书。



从目标设备中删除证书，设备必须已在预配使用 PCp 证书，并该证书的私钥必须驻留在主机中，以便它可以与设备一起传递管理身份验证。

如果删除的 ASC 主机证书 (ASCh)，该工具 ASCh 证书链中删除所有相关的签名者证书 (SCh)。

如果从 ASCh 证书链中删除 SCh 证书，该工具会在证书链中删除指定的 SCh 证书以及其整个父 SCh 证书。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何删除目标设备 ASC 应用商店中两个索引处的证书：

```
EhStorCertMgrCmd /Remove -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:2
```









