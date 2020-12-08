---
title: MSiSCSI \_ SECURITYCONFIGOPERATIONS WMI 类
description: MSiSCSI \_ SECURITYCONFIGOPERATIONS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cdd2b3c877292b495854b114ce2ba01d5784a3de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796441"
---
# <a name="msiscsi_securityconfigoperations-wmi-class"></a>MSiSCSI \_ SECURITYCONFIGOPERATIONS WMI 类


## <span id="ddk_msiscsi_securityconfigoperations_wmi_class_kr"></span><span id="DDK_MSISCSI_SECURITYCONFIGOPERATIONS_WMI_CLASS_KR"></span>


MSiSCSI \_ SECURITYCONFIGOPERATIONS WMI 类定义了发起方为支持 Internet 协议安全 (IPsec) 或质询握手身份验证协议 (CHAP) 而必须实现的安全配置方法。

此外，支持 Internet 密钥交换 (IKE) 与预共享密钥的发起程序必须实现以下方法：

-   [SetPresharedKeyForId](setpresharedkeyforid.md)

-   [GetPresharedKeyForId](getpresharedkeyforid.md)

-   [SetGroupPresharedKey](setgrouppresharedkey.md)

支持 IPsec 预共享密钥和 iSCSI 身份验证凭据的非易失缓存的发起程序 (即，用户名和密码) 必须实现 [ClearCache](clearcache.md) 方法。 发起方还必须通过在 [MSiSCSI \_ HBAInformation WMI 类](msiscsi-hbainformation-wmi-class.md)中设置相应的标志来指示它使用缓存。 具体而言，如果发起程序缓存了预共享密钥，则它应 \_ \_ \_ \_ 在类的 **FunctionalitySupported** 成员中设置 iscsi hba 预共享密钥缓存标志; 如果发起程序缓存 iscsi 身份验证数据，则应设置 iscsi \_ hba \_ ISCSI \_ 身份验证 \_ 缓存标志。

由于 MSiSCSI \_ SecurityConfigOperations 类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理的特定物理设备对象 (PDO) 的名称注册该类。

要使发起程序与 iSCSI 发现服务兼容，必须实现 [SetGenerationalGuid](setgenerationalguid.md) 方法。

对于属于此类的每个方法，托管对象格式 (MOF) 语法在该方法的参考页中进行了介绍。 以下主题介绍了这些方法及其随附的结构：

[ClearCache](clearcache.md)

[GetPresharedKeyForId](getpresharedkeyforid.md)

[SetGenerationalGuid](setgenerationalguid.md)

[SetGroupPresharedKey](setgrouppresharedkey.md)

[SetPresharedKeyForId](setpresharedkeyforid.md)

[SetTunnelModeOuterAddress](settunnelmodeouteraddress.md)

 

 





