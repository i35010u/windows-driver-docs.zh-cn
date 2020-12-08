---
title: /List 开关
description: 增强的存储证书管理工具的/List 开关列出了连接到计算机的所有符合 IEEE 1667 的 USB 存储设备。
keywords:
- /List 交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /List
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b8530c6495509949c210bb546958c55a536b8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785239"
---
# <a name="list-switch"></a>/List 开关


增强的存储证书管理工具的 **/list** 开关列出了连接到计算机的所有符合 IEEE 1667 的 USB 存储设备。 此开关还可用于列出证书 (及其属性) 在指定 USB 存储设备中的身份验证接收器证书 (ASC) 存储区中。

```
    EhStorCertMgrCmd /List [-Volume:
    VolumeName
    ]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span>**-Volume：**   
符合 IEEE 1667 的 USB 存储的卷名。 有关此参数的格式的详细信息，请参阅 [增强的存储证书管理工具概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**注意**  要生成当前连接到计算机的符合 IEEE 1667 的 USB 存储设备的卷名称列表，请在命令提示符下键入 **EhStorCertMgrCmd/list** ，然后按 enter。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

如果使用不带任何参数的 **/list** 开关，则该工具将报告连接到计算机的所有符合 IEEE 1667 的 USB 存储设备。 在这种情况下，只会报告 USB 存储设备的卷名。

有关特定 USB 存储设备的详细信息，请使用 **-Volume** 参数来指定设备。 在这种情况下，该工具将报告设备中 ASC 存储区中存在的证书。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

此示例演示如何列出连接到计算机的符合 IEEE 1667 的 USB 存储设备。

```
EhStorCertMgrCmd /List
```

```
Executing list switch...
Volume Name : \\?\usbstor#ieee1667control&ven_msft&prod_disk_sim_v0.01&rev_0.01#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}
```

此示例显示了如何在与 IEEE 1667 兼容的 USB 存储设备的 ASC 存储区中列出证书的详细信息。

```
EhStorCertMgrCmd.exe /List -Volume:"\\?\usbstor#ieee1667control&ven_msft&prod_disk_sim_v0.01&rev_0.01#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}"
```

```
Executing List operation for specified volume name...
## Certificate Subject             : Microsoft Cert Simulator RSA 1024 SHA-1
---------------------------------
Certificate Index               : 0
Issued To                       : Microsoft Cert Simulator RSA 1024 SHA-1
Issued By                       : Microsoft 1667 Simulator Root
Certificate Expiration Date     : 12/30/9999
Certificate Status              : A certificate chain could not be built to a trusted root authority.

## Certificate Subject             : PCp PKCS SHA-1 1024 no ext
---------------------------------
Certificate Index               : 1
Issued To                       : PCp PKCS SHA-1 1024 no ext
Issued By                       : PCp PKCS SHA-1 1024 no ext
Certificate Expiration Date     : 5/31/2010
Certificate Status              : Certificate is Valid

## Certificate Subject             : HCh PKCS SHA-1 1024 no ext
---------------------------------
Certificate Index               : 2
Issued To                       : HCh PKCS SHA-1 1024 no ext
Issued By                       : HCh PKCS SHA-1 1024 no ext
Certificate Expiration Date     : 5/31/2010
Certificate Status              : Certificate is Valid
```









