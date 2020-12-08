---
title: /Remove 开关
description: 增强的存储证书管理工具的/Remove 开关从身份验证接收器证书中删除指定的证书 (ASC) store in IEEE 1667 兼容 USB 存储设备。请注意，若要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 EhStorCertMgrCmd/List，然后按 Enter。
keywords:
- /Remove 交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /Remove
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b29240204be61ae43d612d285da3eea793c3a57f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803983"
---
# <a name="remove-switch"></a>/Remove 开关


增强的存储证书管理工具的 **/remove** 开关从身份验证接收器证书中删除指定的证书 (ASC) STORE in IEEE 1667 兼容 USB 存储设备。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 **EhStorCertMgrCmd/list** ，然后按 enter。



```
    EhStorCertMgrCmd /Remove  -Volume:
    VolumeName
     -Index:
    IndexValue
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span>**-Volume：**   
目标设备的卷名。 有关此参数的格式的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 **EhStorCertMgrCmd/list** ，然后按 enter。



<span id="_______-Index_______"></span><span id="_______-index_______"></span><span id="_______-INDEX_______"></span>**-Index：**   
ASC 存储中将删除证书的索引。 索引值必须大于1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/Remove** 开关从目标设备中删除除以下证书之外的所有证书：

-   设置证书 (PCp) 。 若要删除 PCp 证书，必须使用 [**/Initialize 开关**](-initialize-switch.md)。

-   ASC-制造商证书 (ASCm) 。

    **注意**   增强的存储证书管理工具无法在目标设备中添加、删除或替换 asc 制造商 (ASCm) 证书。



若要从目标设备中删除证书，必须使用 PCp 证书预配设备，并且该证书的私钥必须位于主机中，以便它可以通过设备管理身份验证。

如果 (ASCh) 中删除 ASC 主机证书，则该工具将删除 ASCh 证书链中 (Sch-m) 的所有相关签名者证书。

如果从 ASCh 证书链中删除 Sch-m 证书，则该工具会删除指定的 Sch-m 证书及其整个父 Sch-m 证书。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例演示如何在目标设备的 ASC 存储区中的索引2处删除证书：

```
EhStorCertMgrCmd /Remove -Volume:"\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}" -Index:2
```









