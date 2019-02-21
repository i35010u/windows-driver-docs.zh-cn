---
title: / 列表开关
description: 增强型存储证书管理工具的 /List 开关列出了所有的 IEEE 1667 合规 USB 存储设备连接到计算机。
ms.assetid: ae0e2991-32db-42b3-839d-83b7e2b8b35f
keywords:
- / 列表交换机驱动程序开发工具
topic_type:
- apiref
api_name:
- /List
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da7b84a0cf06767ae209e6822168982ad87c8f45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521556"
---
# <a name="list-switch"></a>/ 列表开关


**/List**增强存储证书管理工具的开关列出了所有的 IEEE 1667 合规 USB 存储设备连接到计算机。 此开关也可用来列出 （以及它们的属性） 的证书的身份验证接收器证书 (ASC) 存储中指定的 USB 存储设备中。

```
    EhStorCertMgrCmd /List [-Volume:
    VolumeName
    ]
```

## <a name="span-idsubparametersspanspan-idsubparametersspanspan-idsubparametersspansubparameters"></a><span id="Subparameters"></span><span id="subparameters"></span><span id="SUBPARAMETERS"></span>子参数


<span id="_______-Volume_______"></span><span id="_______-volume_______"></span><span id="_______-VOLUME_______"></span> **-卷：**   
IEEE 1667 合规的 USB 存储卷名称。 此参数的格式的详细信息，请参阅[增强存储证书管理工具的概述](overview-of-the-enhanced-storage-certificate-management-tool.md)。

**请注意**若要生成的 IEEE 1667 合规 USB 存储设备的当前连接到计算机的卷名称的列表，请键入**EhStorCertMgrCmd /List**在命令提示符，然后按 Enter。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果您使用 **/list**切换不带任何参数，该工具将报告所有 IEEE 1667 合规 USB 存储设备连接到计算机上。 在这种情况下，报告仅 USB 存储设备的卷名称。

有关特定的 USB 存储设备的详细信息，请使用 **-卷**参数来指定的设备。 在这种情况下，该工具报告 ASC 存储中的设备中存在的证书。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

此示例演示如何列出的 IEEE 1667 合规 USB 存储设备连接到计算机。

```
EhStorCertMgrCmd /List
```

```
Executing list switch...
Volume Name : \\?\usbstor#ieee1667control&ven_msft&prod_disk_sim_v0.01&rev_0.01#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}
```

此示例演示如何列出有关 IEEE 1667 合规 USB 存储设备 ASC 存储区中证书的详细信息。

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









