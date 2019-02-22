---
title: MSiSCSI\_SecurityConfigOperations WMI 类
description: MSiSCSI\_SecurityConfigOperations WMI 类
ms.assetid: 27056bae-ba73-409f-b55e-453ed46a61d2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 19e6e2cb79b5b218e1b90cb0046aff755f685e10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554363"
---
# <a name="msiscsisecurityconfigoperations-wmi-class"></a>MSiSCSI\_SecurityConfigOperations WMI 类


## <span id="ddk_msiscsi_securityconfigoperations_wmi_class_kr"></span><span id="DDK_MSISCSI_SECURITYCONFIGOPERATIONS_WMI_CLASS_KR"></span>


MSiSCSI\_SecurityConfigOperations WMI 类定义发起程序必须实现以支持 Internet 协议安全性 (IPsec) 或质询握手身份验证协议 (CHAP) 的安全配置方法。

此外，支持使用预共享密钥的 Internet 密钥交换 (IKE) 的发起程序必须实现以下方法：

-   [SetPresharedKeyForId](setpresharedkeyforid.md)

-   [GetPresharedKeyForId](getpresharedkeyforid.md)

-   [SetGroupPresharedKey](setgrouppresharedkey.md)

支持非易失性缓存 IPsec 预共享密钥和 iSCSI 身份验证凭据 （即，用户名和密码） 必须实现的发起程序[ClearCache](clearcache.md)方法。 发起方还必须指示它通过设置适当的标记中使用缓存[MSiSCSI\_HBAInformation WMI 类](msiscsi-hbainformation-wmi-class.md)。 具体而言，如果发起方缓存预共享的密钥，它应设置 ISCSI\_HBA\_预共享\_密钥\_中的缓存标志**FunctionalitySupported**类; 的成员如果发起方缓存 iSCSI 身份验证数据，它应设置 ISCSI\_HBA\_ISCSI\_身份验证\_缓存标记。

因为 MSiSCSI\_SecurityConfigOperations 类与存储微型端口驱动程序的特定实例相关联，则微型端口驱动程序必须注册使用特定的物理设备对象 (PDO) 的名称的类的微型端口驱动程序管理。

为发起程序能够与 iSCSI 发现服务兼容，则它必须实现[SetGenerationalGuid](setgenerationalguid.md)方法。

属于此类的每个方法的托管的对象格式 (MOF) 语法所述的方法的参考页。 以下主题介绍了这些方法和其随附的结构：

[ClearCache](clearcache.md)

[GetPresharedKeyForId](getpresharedkeyforid.md)

[SetGenerationalGuid](setgenerationalguid.md)

[SetGroupPresharedKey](setgrouppresharedkey.md)

[SetPresharedKeyForId](setpresharedkeyforid.md)

[SetTunnelModeOuterAddress](settunnelmodeouteraddress.md)

 

 





