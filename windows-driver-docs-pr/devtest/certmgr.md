---
title: CertMgr
description: CertMgr (Certmgr.exe) 是一个命令行的 CryptoAPI 工具，管理证书、 证书信任列表 (Ctl) 和证书吊销列表 (Crl)。
ms.assetid: 860693f5-de64-4ca9-be64-23e2fbb862c5
keywords:
- CertMgr 驱动程序开发工具
topic_type:
- apiref
api_name:
- CertMgr
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e68db909d8b8f99f148e179dd9bcda1417230247
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371615"
---
# <a name="certmgr"></a>CertMgr


CertMgr (Certmgr.exe) 是一个命令行[CryptoAPI](https://go.microsoft.com/fwlink/p/?linkid=136391)管理证书、 证书信任列表 (Ctl) 和证书吊销列表 (Crl) 的工具。

CertMgr 支持大量的开关，但本部分介绍了仅与管理相关的那些[测试证书](https://docs.microsoft.com/windows-hardware/drivers/install/test-certificates)证书存储中。

```
    CertMgr [/add|/del|/put] [Switches] [/s [/r RegistryLocation ] ] SourceName [/s [/r RegistryLocation] ] [DestinationName]
```

### <a name="span-idpartiallistofoperationsswitchesandargumentsspanspan-idpartiallistofoperationsswitchesandargumentsspanpartial-list-of-operations-switches-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、 开关和参数的部分列表

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>操作

<span id="add"></span><span id="ADD"></span>**add**  
配置 CertMgr 若要从指定的文件添加证书、 Ctl 或 Crl *SourceName*指定的证书存储到*DestinationName*。

<span id="del"></span><span id="DEL"></span>**del**  
配置要删除证书、 Ctl 或 Crl 由指定的证书存储中的 CertMgr *SourceName*从指定的证书存储*DestinationName*。 如果*DestinationName*未指定，则*SourceName*也将用作目标存储区并将进行相应修改。

<span id="put"></span><span id="PUT"></span>**put**  
将配置保存证书、 Ctl 或 Crl 从指定的证书存储的 CertMgr *SourceName*到指定的文件*DestinationName*。

<span id="none"></span><span id="NONE"></span>无  
CertMgr 中的证书存储区或文件指定如果未不指定任何命令，显示所有证书、 Ctl 或 Crl *SourceName*。

### <a name="span-idswitchesandargumentsspanspan-idswitchesandargumentsspanswitches-and-arguments"></a><span id="switches_and_arguments"></span><span id="SWITCHES_AND_ARGUMENTS"></span>开关和参数

<span id="_c"></span><span id="_C"></span> **/c**  
配置仅处理从指定的文件的证书的 CertMgr *SourceName*。

<span id="_CTL"></span><span id="_ctl"></span> **/CTL**  
配置 CertMgr 仅处理从指定的文件的 Ctl *SourceName*。

<span id="_CRL"></span><span id="_crl"></span> **/CRL**  
配置 CertMgr 仅处理从指定的文件的 Crl *SourceName*。

<span id="_s"></span><span id="_S"></span> **/s**  
配置访问指定的证书存储的 CertMgr *SourceName*或*DestinationName*作为系统存储。

<span id="_r_registryLocation"></span><span id="_r_registrylocation"></span><span id="_R_REGISTRYLOCATION"></span> **/r** *registryLocation*  
指定系统证书存储的注册表位置。 **/R**交换机才与一起使用时有效 **/s**切换。 *RegistryLocation*参数必须是：

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
指定的注册表位置 HKEY\_当前\_用户。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
指定的注册表位置 HKEY\_本地\_机。

如果 **/r**交换机未指定连同 **/s**切换，请*currentUser*是默认值。

有关这些证书存储区的详细信息，请参阅[证书存储区](https://docs.microsoft.com/windows-hardware/drivers/install/certificate-stores)。

<span id="_v"></span><span id="_V"></span> **/v**  
配置 CertMgr 以显示有关证书、 Ctl 和 Crl 的详细的信息。 如果未指定此开关，CertMgr 仅显示的信息摘要。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

若要使用 CertMgr，用户必须是系统上的 Administrators 组的成员并从提升的命令提示符运行命令。

有关 CertMgr 参数的完整列表，请参阅[证书管理器工具](https://go.microsoft.com/fwlink/p/?linkid=70233)网站。

CertMgr 工具的 32 位版本位于*bin\\i386* WDK 的文件夹。 该工具的 64 位版本位于 bin\\amd64 和 bin\\WDK 的 ia64 文件夹。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

以下两个 CertMgr 命令在文件中添加证书*OutputFile.cer*到受信任的根证书颁发机构证书存储区和受信任的发行者证书存储区。

```
CertMgr /add OutputFile.cer /s /r localMachine root 
CertMgr /add OutputFile.cer /s /r localMachine trustedpublisher
```

 

 





