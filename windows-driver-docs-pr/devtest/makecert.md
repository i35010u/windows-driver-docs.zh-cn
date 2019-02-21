---
title: MakeCert
description: MakeCert (Makecert.exe) 是命令行的 CryptoAPI 工具，用于创建系统测试的根键或另一个指定密钥签名的 X.509 证书。
ms.assetid: 752aa806-5e8c-4519-bece-dcd91161b98a
keywords:
- MakeCert 驱动程序开发工具
topic_type:
- apiref
api_name:
- MakeCert
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ded3ef7bebd2ba653e12b9c9efb5269fe4cde9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526641"
---
# <a name="makecert"></a>MakeCert


MakeCert (Makecert.exe) 是一个命令行[CryptoAPI](https://go.microsoft.com/fwlink/p/?linkid=136391)工具，用于创建系统测试的根键或由另一个签名的 X.509 证书指定的密钥。 该证书将证书名称绑定到的密钥对的公共部分。 将证书保存到文件和 / 或系统证书存储区。

MakeCert 支持大量的开关，但本部分仅介绍了与创建相关的基本开关[测试证书](https://msdn.microsoft.com/library/windows/hardware/ff548693)，可用于测试签名[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff544840)或嵌入中的驱动程序文件的签名。

```
    MakeCert [/b DateStart] [/e DateEnd] [/len KeyLength] [/m nMonths] [/n "Name"] [/pe] [/r] [/sc SubjectCertFile] [/sk SubjectKey] [/sr SubjectCertStoreLocation] [/ss SubjectCertStoreName] [/sv SubjectKeyFile]OutputFile
```

### <a name="span-idpartiallistofswitchesandargumentsspanspan-idpartiallistofswitchesandargumentsspanpartial-list-of-switches-and-arguments"></a><span id="partial_list_of_switches_and_arguments"></span><span id="PARTIAL_LIST_OF_SWITCHES_AND_ARGUMENTS"></span>开关和参数的部分列表

<span id="_b_DateStart"></span><span id="_b_datestart"></span><span id="_B_DATESTART"></span>**/b** *DateStart*  
指定当证书首先开始生效的开始日期。 格式*DateStart*为 mm/dd/yyyy。

如果**b </b**开关不指定，默认开始日期为创建的证书时的日期。

<span id="_e_DateEnd"></span><span id="_e_dateend"></span><span id="_E_DATEEND"></span>**/e** *DateEnd*  
指定当证书的有效期结束时的结束日期。 格式*DateEnd*为 mm/dd/yyyy。

如果 **/e**开关不指定，默认结束日期为 12/31/2039年。

<span id="_len_KeyLength"></span><span id="_len_keylength"></span><span id="_LEN_KEYLENGTH"></span>**/len** *KeyLength*  
使用者的专用和公用密钥的位为单位为单位指定的长度。

如果不指定 /len 开关，默认的密钥长度为 1024 位。

<span id="_m_nMonths"></span><span id="_m_nmonths"></span><span id="_M_NMONTHS"></span>**/m** *nMonths*  
指定从在此期间该证书会保持有效的开始日期开始月的数。

<span id="_n__Name_"></span><span id="_n__name_"></span><span id="_N__NAME_"></span>**/n** "<em>Name</em>**"**  
指定证书的名称。 此名称必须符合 X.500 标准。 最简单方法是使用"CN =*MyName*"格式。

如果 **/n**不指定开关，该证书的默认名称为"Joe 的软件 Emporium"。

<span id="_pe"></span><span id="_PE"></span>**/pe**  
配置 MakeCert 来使私钥可导出证书相关联。

<span id="_r"></span><span id="_R"></span>**/r**  
配置 MakeCert 创建自签名的根证书。

<span id="_sc_SubjectCertFile"></span><span id="_sc_subjectcertfile"></span><span id="_SC_SUBJECTCERTFILE"></span>**/sc** *SubjectCertFile*  
指定使用者的证书文件名称以及使用的现有使用者公共密钥。

<span id="_sk_SubjectKey"></span><span id="_sk_subjectkey"></span><span id="_SK_SUBJECTKEY"></span>**/sk** *SubjectKey*  
指定持有私钥的使用者的密钥容器的名称。 如果密钥容器不存在，将创建新的密钥容器。 如果既没有 **/sk**也不 **/sv**切换输入，则默认密钥容器是创建和使用的默认值。

<span id="_sr_SubjectCertStoreLocation"></span><span id="_sr_subjectcertstorelocation"></span><span id="_SR_SUBJECTCERTSTORELOCATION"></span>**/sr** *SubjectCertStoreLocation*  
指定的证书存储区的注册表位置。 *SubjectCertStoreLocation*参数必须为下列操作之一：

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
指定的注册表位置 HKEY\_当前\_用户。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
指定的注册表位置 HKEY\_本地\_机。

如果 **/r**交换机未指定连同 **/s**切换，请*currentUser*是默认值。

<span id="_ss_SubjectCertStoreName"></span><span id="_ss_subjectcertstorename"></span><span id="_SS_SUBJECTCERTSTORENAME"></span>**/ss** *SubjectCertStoreName*  
指定保存生成的证书的证书存储区的名称。

<span id="_sv_SubjectKeyFile"></span><span id="_sv_subjectkeyfile"></span><span id="_SV_SUBJECTKEYFILE"></span>**/sv** *SubjectKeyFile*  
指定持有私钥的使用者的.pvk 文件的名称。 如果既没有 **/sk**也不 **/sv**切换输入，则默认密钥容器是创建和使用的默认值。

<span id="OutputFile"></span><span id="outputfile"></span><span id="OUTPUTFILE"></span>*OutputFile*  
在其中保存生成的证书文件的名称。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

MakeCert 支持大量的开关。 本主题中所述的开关都限制为可用于创建的那些[测试证书](https://msdn.microsoft.com/library/windows/hardware/ff548693)。

MakeCert 参数的完整列表，请参阅[MakeCert](https://go.microsoft.com/fwlink/p/?linkid=62653)网站并[使用 MakeCert](https://go.microsoft.com/fwlink/p/?linkid=62655)网站。

MakeCert 工具的 32 位版本位于 bin\\WDK 的 i386 文件夹。 该工具的 64 位版本位于 bin\\amd64 和 bin\\WDK 的 ia64 文件夹。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

在以下示例中，MakeCert 命令将生成一个名为"Contoso.com(Test)，"安装测试证书在 PrivateCertStore 证书存储中，并创建 Testcert.cer 文件，其中包含一份该测试的自签名的测试证书证书。

```
MakeCert -r -pe -ss PrivateCertStore -n "CN=Contoso.com(Test)" testcert.cer
```

 

 





