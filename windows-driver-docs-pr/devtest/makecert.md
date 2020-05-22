---
title: MakeCert
description: MakeCert （Makecert）是一个命令行 CryptoAPI 工具，用于创建由系统测试根密钥或其他指定的密钥签名的 x.509 证书。
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
ms.openlocfilehash: c55b60f65a0b7a229948996fab045b7445b0d829
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769631"
---
# <a name="makecert"></a>MakeCert


MakeCert （Makecert）是一个命令行[CryptoAPI](https://docs.microsoft.com/windows/win32/seccrypto/cryptography-portal)工具，用于创建由系统测试根密钥或其他指定的密钥签名的 x.509 证书。 证书将证书名称绑定到密钥对的公共部分。 证书将保存到文件和/或系统证书存储。

MakeCert 支持大量交换机，但本节仅介绍与创建[测试证书](https://docs.microsoft.com/windows-hardware/drivers/install/makecert-test-certificate)相关的基本交换机，该证书可用于对[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)进行测试签名或将签名嵌入驱动程序文件。

```
    MakeCert [/b DateStart] [/e DateEnd] [/len KeyLength] [/m nMonths] [/n "Name"] [/pe] [/r] [/sc SubjectCertFile] [/sk SubjectKey] [/sr SubjectCertStoreLocation] [/ss SubjectCertStoreName] [/sv SubjectKeyFile]OutputFile
```

### <a name="span-idpartial_list_of_switches_and_argumentsspanspan-idpartial_list_of_switches_and_argumentsspanpartial-list-of-switches-and-arguments"></a><span id="partial_list_of_switches_and_arguments"></span><span id="PARTIAL_LIST_OF_SWITCHES_AND_ARGUMENTS"></span>开关和参数的部分列表

<span id="_b_DateStart"></span><span id="_b_datestart"></span><span id="_B_DATESTART"></span>**/B** *DateStart*  
指定证书首次变为有效的起始日期。 *DateStart*的格式为 mm/dd/yyyy。

如果未指定 **/b**开关，则默认开始日期为创建证书的日期。

<span id="_e_DateEnd"></span><span id="_e_dateend"></span><span id="_E_DATEEND"></span>**/E** *DateEnd*  
指定证书有效期结束的结束日期。 *DateEnd*的格式为 mm/dd/yyyy。

如果未指定 **/e**交换机，则默认结束日期为12/31/2039。

<span id="_len_KeyLength"></span><span id="_len_keylength"></span><span id="_LEN_KEYLENGTH"></span>**/Len** *KeyLength*  
指定使用者的私钥和公钥的长度，单位为位。

如果未指定/len 开关，则默认密钥长度为1024位。

<span id="_m_nMonths"></span><span id="_m_nmonths"></span><span id="_M_NMONTHS"></span>**/M** *nMonths*  
指定从开始日期开始，证书将保持有效的月数。

<span id="_n__Name_"></span><span id="_n__name_"></span><span id="_N__NAME_"></span>**/n**"<em>Name</em>**"**  
指定证书的名称。 此名称必须符合 X.500 标准。 最简单的方法是使用 "CN =*MyName*" 格式。

如果未指定 **/n**开关，则证书的默认名称为 "Joe Of Software Emporium"。

<span id="_pe"></span><span id="_PE"></span>**/pe**  
配置 MakeCert 以使与证书关联的私钥可导出。

<span id="_r"></span><span id="_R"></span>**/r**  
配置 MakeCert 以创建自签名根证书。

<span id="_sc_SubjectCertFile"></span><span id="_sc_subjectcertfile"></span><span id="_SC_SUBJECTCERTFILE"></span>**/Sc** *SubjectCertFile*  
指定主题的证书文件名以及使用的现有使用者公钥。

<span id="_sk_SubjectKey"></span><span id="_sk_subjectkey"></span><span id="_SK_SUBJECTKEY"></span>**/Sk** *SubjectKey*  
指定保存私钥的主题密钥容器的名称。 如果密钥容器不存在，则将创建新的密钥容器。 如果未输入 **/sk**和 **/sv**交换机，则默认情况下会创建并使用默认的密钥容器。

<span id="_sr_SubjectCertStoreLocation"></span><span id="_sr_subjectcertstorelocation"></span><span id="_SR_SUBJECTCERTSTORELOCATION"></span>**/Sr** *SubjectCertStoreLocation*  
指定证书存储的注册表位置。 *SubjectCertStoreLocation*参数必须是以下内容之一：

<span id="currentUser"></span><span id="currentuser"></span><span id="CURRENTUSER"></span>*currentUser*  
指定 HKEY 当前用户的注册表位置 \_ \_ 。

<span id="localMachine"></span><span id="localmachine"></span><span id="LOCALMACHINE"></span>*localMachine*  
指定本地计算机的注册表位置 HKEY \_ \_ 。

如果 **/r**开关与 **/s**开关一起指定，则默认值为*currentUser* 。

<span id="_ss_SubjectCertStoreName"></span><span id="_ss_subjectcertstorename"></span><span id="_SS_SUBJECTCERTSTORENAME"></span>**/Ss** *SubjectCertStoreName*  
指定在其中保存生成的证书的证书存储的名称。

<span id="_sv_SubjectKeyFile"></span><span id="_sv_subjectkeyfile"></span><span id="_SV_SUBJECTKEYFILE"></span>**/Sv** *SubjectKeyFile*  
指定保存私钥的主题的 pvk 文件的名称。 如果未输入 **/sk**和 **/sv**交换机，则默认情况下会创建并使用默认的密钥容器。

<span id="OutputFile"></span><span id="outputfile"></span><span id="OUTPUTFILE"></span>*OutputFile*  
在其中保存生成的证书的文件的名称。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

MakeCert 支持大量交换机。 本主题中所述的开关仅限于可用于创建[测试证书](https://docs.microsoft.com/windows-hardware/drivers/install/makecert-test-certificate)的开关。

有关 MakeCert 参数的完整列表，请参阅[MakeCert](https://docs.microsoft.com/windows/win32/seccrypto/makecert)网站和[使用 MakeCert](https://docs.microsoft.com/windows/win32/seccrypto/using-makecert)网站。

MakeCert 工具的32位版本位于 WDK 的 bin \\ i386 文件夹中。 此工具的64位版本位于 WDK 的 bin \\ 和 bin \\ ia64 文件夹中。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

在下面的示例中，MakeCert 命令生成名为 "Contoso .com （Test）" 的自签名测试证书，在 PrivateCertStore 证书存储中安装测试证书，并创建 Testcert 文件，其中包含测试证书的副本。

```
MakeCert -r -pe -ss PrivateCertStore -n "CN=Contoso.com(Test)" testcert.cer
```

 

 





