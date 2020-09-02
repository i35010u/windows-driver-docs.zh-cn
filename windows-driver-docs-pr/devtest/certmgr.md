---
title: CertMgr
description: 'Certmgr.msc ( # A0) 是一个命令行 CryptoAPI 工具，用于管理证书、证书信任列表 (Ctl) 和证书吊销列表 (Crl) 。'
ms.assetid: 860693f5-de64-4ca9-be64-23e2fbb862c5
keywords:
- Certmgr.msc 驱动程序开发工具
topic_type:
- apiref
api_name:
- CertMgr
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2db6eb393de0b4f7b08fca7f34cdf642bd7aadef
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382284"
---
# <a name="certmgr"></a>CertMgr


Certmgr.msc ( # A0) 是一个命令行 [CryptoAPI](/windows/win32/seccrypto/cryptography-portal) 工具，用于管理证书、证书信任列表 (ctl) 和证书吊销列表 (crl) 。

Certmgr.msc 支持大量交换机，但本部分仅介绍与管理证书存储中的 [测试证书](../install/makecert-test-certificate.md) 相关的参数。

```
    CertMgr [/add|/del|/put] [Switches] [/s [/r RegistryLocation ] ] SourceName [/s [/r RegistryLocation] ] [DestinationName]
```

### <a name="span-idpartial_list_of_operations__switches__and_argumentsspanspan-idpartial_list_of_operations__switches__and_argumentsspanpartial-list-of-operations-switches-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、开关和参数的部分列表

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>运算符

<span id="add"></span><span id="ADD"></span>**把**  
将 Certmgr.msc 配置为将证书、Ctl 或 Crl *指定的文件* 从使用情况指定的文件添加到 *DestinationName*指定的证书存储中。

<span id="del"></span><span id="DEL"></span>**del**  
将 Certmgr.msc 配置为在证书存储区中删除由*DestinationName*指定的证书存储区*中的证书*、ctl 或 crl。 如果未指定 *DestinationName* ，则会将其作为目标存储 *区，并* 将进行相应修改。

<span id="put"></span><span id="PUT"></span>**准备**  
将 Certmgr.msc 配置为将证书、Ctl 或 Crl 从证书存储区 *指定的证书存储保存到* *DestinationName*指定的文件。

<span id="none"></span><span id="NONE"></span>内容  
如果未指定任何命令，则 Certmgr.msc 会在证书存储或证书的指定文件中显示所有证书、Ctl 或*crl。*

### <a name="span-idswitches_and_argumentsspanspan-idswitches_and_argumentsspanswitches-and-arguments"></a><span id="switches_and_arguments"></span><span id="SWITCHES_AND_ARGUMENTS"></span>开关和参数

<span id="_c"></span><span id="_C"></span>**/c**  
将 Certmgr.msc 配置为仅处理由证书的*指定的文件的证书。*

<span id="_CTL"></span><span id="_ctl"></span>**/CTL**  
将 Certmgr.msc 配置为仅处理由 "" 指定 *的文件*中的 ctl。

<span id="_CRL"></span><span id="_crl"></span>**/CRL**  
将 Certmgr.msc 配置为仅 *处理因其*指定的文件中的 crl。

<span id="_s"></span><span id="_S"></span>**/s**  
将 Certmgr.msc 配置为访问由或*DestinationName*指定为系统*存储的证书*存储区。

<span id="_r_registryLocation"></span><span id="_r_registrylocation"></span><span id="_R_REGISTRYLOCATION"></span>**/R** *registryLocation*  
指定系统证书存储的注册表位置。 **/R**开关仅在与 **/s**开关一起使用时才有效。 *RegistryLocation*参数必须是：

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
指定 HKEY 当前用户的注册表位置 \_ \_ 。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
指定本地计算机的注册表位置 HKEY \_ \_ 。

如果 **/r** 开关与 **/s** 开关一起指定，则默认值为 *currentUser* 。

有关这些证书存储的详细信息，请参阅 [证书存储](../install/certificate-stores.md)。

<span id="_v"></span><span id="_V"></span>**/v**  
配置 Certmgr.msc 以显示有关证书、Ctl 和 Crl 的详细信息。 如果未指定此开关，Certmgr.msc 只显示简短信息。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

若要使用 Certmgr.msc，用户必须是系统上 Administrators 组的成员，并从提升的命令提示符运行该命令。

有关 Certmgr.msc 参数的完整列表，请参阅 [证书管理器工具](/dotnet/framework/tools/certmgr-exe-certificate-manager-tool) 网站。

Certmgr.msc 工具的32位版本位于 WDK 的 *bin \\ i386* 文件夹中。 此工具的64位版本位于 WDK 的 bin \\ 和 bin \\ ia64 文件夹中。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

以下两个 Certmgr.msc 命令将 *OutputFile* 文件中的证书添加到 "受信任的根证书颁发机构" 证书存储和 "受信任的发布者" 证书存储中。

```
CertMgr /add OutputFile.cer /s /r localMachine root 
CertMgr /add OutputFile.cer /s /r localMachine trustedpublisher
```

 

