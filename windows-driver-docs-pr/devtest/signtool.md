---
title: SignTool
description: SignTool (Signtool.exe) 是该进行数字签名文件的命令行的 CryptoAPI 工具，验证文件和时间戳文件中的签名。
ms.assetid: c1006c07-f204-4fc0-8f99-36e69cbee96d
keywords:
- SignTool 驱动程序开发工具
topic_type:
- apiref
api_name:
- SignTool
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9446fc4037b1717ad23306f9751248a4a5fffd22
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374416"
---
# <a name="signtool"></a>SignTool


SignTool (Signtool.exe) 是一个命令行[CryptoAPI](https://go.microsoft.com/fwlink/p/?linkid=136391)工具进行数字签名文件中，验证文件和时间戳文件中的签名。

```
    SignTool [Operation] [Options] [FileName ...]
```

### <a name="span-idpartiallistofoperationsswitchesandargumentsspanspan-idpartiallistofoperationsswitchesandargumentsspanpartial-list-of-operations-options-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、 选项和参数的部分列表

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>操作

<span id="catdb"></span><span id="CATDB"></span>**catdb**  
配置 SignTool 更新目录数据库。 SignTool 向数据库添加目录文件，或从数据库中删除目录。 默认情况下**catdb**命令将添加的文件，通过指定其名称*FileName*参数，系统组件 （驱动程序） 数据库。

**请注意**  目录数据库用于自动查找目录文件。

 

<span id="sign"></span><span id="SIGN"></span>**sign**  
对数字签名文件的已指定了名称配置 SignTool*文件名*参数。

<span id="timestamp"></span><span id="TIMESTAMP"></span>**timestamp**  
为时间戳的已指定了名称的文件配置 SignTool*文件名*参数。

<span id="verify"></span><span id="VERIFY"></span>**verify**  
配置 SignTool 验证其名称指定的文件的数字签名*文件名*参数。

### <a name="span-idcatdboperationswitchesspanspan-idcatdboperationswitchesspancatdb-operation-options"></a><span id="catdb_operation_switches"></span><span id="CATDB_OPERATION_SWITCHES"></span>Catdb 操作选项

<span id="_d"></span><span id="_D"></span> **/d**  
配置 SignTool 更新目录数据库。 如果既没有 **/d**也不 **/g**使用选项，则 SignTool 更新系统组件和驱动程序数据库。

<span id="_g_Guid"></span><span id="_g_guid"></span><span id="_G_GUID"></span> **/g** *Guid*  
配置 SignTool 更新由标识的目录数据库*GUID*参数。

<span id="_r"></span><span id="_R"></span> **/r**  
配置 SignTool 以删除每个目录文件，通过指定其名称*文件名*参数，从目录数据库。 如果未指定此选项，SignTool 将指定的目录文件添加到目录数据库。

<span id="_u"></span><span id="_U"></span> **/u**  
配置 SignTool 生成的唯一名称，如有必要，目录文件，以避免与现有目录文件的目录数据库中的冲突。 如果未指定此选项，SignTool 将覆盖与所添加的目录同名的任何现有目录。

### <a name="span-idsignoperationswitchesspanspan-idsignoperationswitchesspansign-operation-options"></a><span id="sign_operation_switches"></span><span id="SIGN_OPERATION_SWITCHES"></span>签名操作选项

<span id="_a_"></span><span id="_A_"></span> **/a**   
配置 SignTool 将自动选择最佳签名证书。 如果此选项不存在，SignTool 期望找到只有一个签名证书。

<span id="_ac_CrossCertFileName"></span><span id="_ac_crosscertfilename"></span><span id="_AC_CROSSCERTFILENAME"></span> **/ac** *CrossCertFileName*  
指定使用名为软件发行者证书 (SPC) 使用的交叉证书文件的名称*CertificateName*且已安装的证书存储中*StoreName*。 如果签名证书，则一个 SPC，仅应使用此选项。

<span id="_c_CertTemplateName"></span><span id="_c_certtemplatename"></span><span id="_C_CERTTEMPLATENAME"></span> **/c** *CertTemplateName*  
指定签名证书的证书模板名称 （一个 Microsoft 扩展）。

<span id="_csp_CSPName"></span><span id="_csp_cspname"></span><span id="_CSP_CSPNAME"></span> **/csp** *CSPName*  
指定包含私钥容器的加密服务提供程序 (CSP)。

<span id="_d_Desc"></span><span id="_d_desc"></span><span id="_D_DESC"></span> **/d** *Desc*  
指定已签名内容的说明。

<span id="_du_URL"></span><span id="_du_url"></span><span id="_DU_URL"></span> **/du** *URL*  
指定已签名内容的详细说明的 URL。

<span id="_f_SignCertFile"></span><span id="_f_signcertfile"></span><span id="_F_SIGNCERTFILE"></span> **/f** *SignCertFile*  
在文件中指定的签名证书。 支持仅个人信息交换 (PFX) 文件格式。 可以使用[ **Pvk2Pfx** ](pvk2pfx.md)工具来转换 SPC 和 PVK 文件为 PFX 格式。

如果该文件受密码保护的 PFX 格式，请使用 **/p**选项以指定的密码。 如果该文件不包含私钥，使用 **/csp**并 **/k**选项，以分别指定 CSP 和私钥容器名。

<span id="_fd"></span><span id="_FD"></span> **/fd**  
指定要用于创建文件签名的文件摘要算法。 默认值为 SHA1。

<span id="_i_IssuerName"></span><span id="_i_issuername"></span><span id="_I_ISSUERNAME"></span> **/i** *IssuerName*  
指定签名证书的颁发者的名称。 此值可以是整个颁发者名称的子字符串。

<span id="_j_DLL"></span><span id="_j_dll"></span><span id="_J_DLL"></span> **/j** *DLL*  
指定提供的属性的签名的 DLL 的名称。

<span id="_jp_ParameterName"></span><span id="_jp_parametername"></span><span id="_JP_PARAMETERNAME"></span> **/jp** *ParameterName*  
指定的参数传递给由指定的 DLL **/j**命令。

<span id="_kc_PrivKeyContainerName"></span><span id="_kc_privkeycontainername"></span><span id="_KC_PRIVKEYCONTAINERNAME"></span> **/kc** *PrivKeyContainerName*  
指定私钥的密钥容器名称。

<span id="_n_SubjectName"></span><span id="_n_subjectname"></span><span id="_N_SUBJECTNAME"></span> **/n** *SubjectName*  
指定签名证书的使用者的名称。 此值可以是整个主题名称的子字符串。

<span id="_nph"></span><span id="_NPH"></span> **/nph**  
如果支持，则取消可执行文件的页面哈希。 默认值由 SIGNTOOL\_页\_哈希环境变量和 wintrust.dll 版本决定。 对于非 PE 文件，则忽略此选项。

<span id="_p_Password"></span><span id="_p_password"></span><span id="_P_PASSWORD"></span> **/p** *Password*  
指定打开 PFX 文件时要使用的密码。 可以通过使用指定的 PFX 文件 **/f**选项

<span id="_p7__Path"></span><span id="_p7__path"></span><span id="_P7__PATH"></span> **/p7** *Path*  
指定的公钥加密标准 (PKCS) \#7 文件生成对于每个指定的内容文件。 PKCS \#7 文件命名为路径\\filename.p7。

<span id="_p7ce_Value"></span><span id="_p7ce_value"></span><span id="_P7CE_VALUE"></span> **/p7ce** *Value*  
指定用于签名的 PKCS 选项\#7 内容。 将值设置为"嵌入的"可将已签名的内容嵌入 PKCS \#7 文件，或为"DetachedSignedData"以便生成分离的 PKCS 的已签名的数据部分\#7 文件。 如果 **/p7ce**不使用选项，默认情况下将嵌入已签名的内容。

<span id="_p7co__OID"></span><span id="_p7co__oid"></span><span id="_P7CO__OID"></span> **/p7co** *OID*  
指定的对象标识符 (OID)，用于标识已签名的 PKCS \#7 内容。

<span id="_ph___"></span><span id="_PH___"></span> **/ph**   
如果支持，将生成可执行文件的页面哈希。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span> **/r** *RootSubjectName*  
指定签名证书必须链接到的根证书的使用者名称。 此值可以是根证书的整个主题名称的子字符串。

<span id="_s_StoreName"></span><span id="_s_storename"></span><span id="_S_STORENAME"></span> **/s** *StoreName*  
指定要打开搜索要使用的签名文件的证书时的证书存储区的名称。 如果未指定此选项，**我**打开证书存储。

<span id="_sha1_Hash"></span><span id="_sha1_hash"></span><span id="_SHA1_HASH"></span> **/sha1** *哈希*  
指定签名证书的 SHA1 哈希。

<span id="_sm"></span><span id="_SM"></span> **/sm**  
配置 SignTool 将使用计算机证书存储，而不是用户证书存储。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span> **/t** *URL*  
指定时间戳服务器的 URL。 如果未提供此选项，已签名的文件不包含时间戳。 目录文件或驱动程序文件应该是加盖时间戳，因为时间戳签名者的密钥已泄漏，如果使吊销用于对文件进行签名的密钥所需的信息。

<span id="_td____alg"></span><span id="_TD____ALG"></span> **/td** *alg*  
使用/t 选项用于请求 RFC 3161 时间戳服务器使用的摘要算法。

<span id="_tr___URL"></span><span id="_tr___url"></span><span id="_TR___URL"></span> **/tr** *URL*  
指定 RFC 3161 时间戳服务器的 URL。 如果此选项 (或 **/t**) 不是存在，已签名的文件不会带时间戳。 如果时间戳操作失败，将生成一条警告。 此选项不能用于 **/t**选项。

<span id="_u___Usage"></span><span id="_u___usage"></span><span id="_U___USAGE"></span> **/u** *使用情况*  
指定签名证书中必须存在的增强型密钥用法 (EKU)。 可以通过 OID 或字符串指定的用法值。 默认用法为"Code Signing"(1.3.6.1.5.5.7.3.3)。

<span id="_uw_"></span><span id="_UW_"></span> **/uw**   
指定"Windows 系统组件验证"(1.3.6.1.4.1.311.10.3.6) 的用法。

### <a name="span-idtimestampoperationswitchesspanspan-idtimestampoperationswitchesspantimestamp-operation-options"></a><span id="timestamp_operation_switches"></span><span id="TIMESTAMP_OPERATION_SWITCHES"></span>时间戳操作选项

<span id="_p7_"></span><span id="_P7_"></span> **/p7**   
时间戳 PKCS \#7 文件。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span> **/t** *URL*  
指定的时间戳服务器的 URL。 正在加盖时间戳的文件必须具有已签名之前

<span id="_td___alg"></span><span id="_TD___ALG"></span> **/td** *alg*  
请求 RFC 3161 时间戳服务器使用的摘要算法。 **/ t d**用于 **/tr**选项。

<span id="_tp__index"></span><span id="_TP__INDEX"></span> **/tp** *index*  
索引处的签名进行时间戳。

<span id="_tr___alg"></span><span id="_TR___ALG"></span> **/tr** *alg*  
请求 RFC 3161 时间戳服务器使用的摘要算法。 **/ t d**用于 **/tr**选项。

### <a name="span-idverifyoperationswitchesspanspan-idverifyoperationswitchesspanverify-operation-options"></a><span id="verify_operation_switches"></span><span id="VERIFY_OPERATION_SWITCHES"></span>验证操作选项

<span id="_a"></span><span id="_A"></span> **/a**  
指定的所有方法可以都用于验证该文件。 首先，搜索目录数据库以确定是否对文件进行签名在目录中。 如果该文件未签名的任何目录中，SignTool 将尝试验证文件的嵌入的签名。 正在验证文件，可能会也可能不在目录中签名时建议使用此选项。

<span id="_ad"></span><span id="_AD"></span> **/ad**  
指定默认的目录数据库为搜索该文件已签名中的目录。

<span id="_all"></span><span id="_ALL"></span> **/all**  
验证包含多个签名的文件中的所有签名。

<span id="_as"></span><span id="_AS"></span> **/as**  
指定仅对系统组件 （驱动程序） 目录数据库进行搜索该文件已签名中的目录。

<span id="_ag_CatDBGUID"></span><span id="_ag_catdbguid"></span><span id="_AG_CATDBGUID"></span> **/ag** *CatDBGUID*  
指定仅标识的目录数据库，通过*CatDBGUID*参数，搜索该文件已签名中的目录。

<span id="_c___CatalogFileName"></span><span id="_c___catalogfilename"></span><span id="_C___CATALOGFILENAME"></span> **/c** *CatalogFileName*  
指定目录文件的名称。

<span id="_d___"></span><span id="_D___"></span> **/d**   
指定签名工具应打印描述和描述的 URL。

<span id="_ds___index"></span><span id="_DS___INDEX"></span> **/ds** *index*  
验证指定位置处的签名。

<span id="_hash__SHA1SHA256"></span><span id="_hash__sha1sha256"></span><span id="_HASH__SHA1SHA256"></span> **/ 哈希**{**SHA1**|**SHA256**}  
指定要搜索在目录中的文件时使用的可选哈希算法。

<span id="_kp"></span><span id="_KP"></span> **/kp**  
配置 SignTool 将验证指定的文件的数字签名*文件名*参数符合[内核模式代码签署策略](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-policy--windows-vista-and-later-)和[即插即用设备安装签名要求](https://docs.microsoft.com/windows-hardware/drivers/install/pnp-device-installation-signing-requirements--windows-vista-and-later-)的 Windows Vista 和更高版本的 Windows。 如果未指定此选项，SignTool 仅验证签名符合即插即用设备安装签名要求。

<span id="_ms"></span><span id="_MS"></span> **/ms**  
使用多个验证语义。 这是默认行为[ **WinVerifyTrust 函数**](https://docs.microsoft.com/windows/desktop/api/wintrust/nf-wintrust-winverifytrust)调用在 Windows 8 和更高版本。

<span id="_o_Version"></span><span id="_o_version"></span><span id="_O_VERSION"></span> **/o** *版本*  
验证根据操作系统版本的文件。 格式*版本*自变量是<em>PlatformID</em> **:** <em>VerMajor</em> **。** <em>VerMinor</em> **。** <em>BuildNumber</em>

利用 **/o**建议选项。 如果 **/o**未指定，则 SignTool 可能返回意外的结果。 例如，如果不包括 **/o**选项，在较旧版本的操作系统正确验证的系统目录可能无法正确验证更高版本的操作系统上。

<span id="_p7"></span><span id="_P7"></span> **/p7**  
验证 PKCS \#7 文件。 任何现有策略用于 PKCS \#7 验证。 检查该签名和签名证书生成了链。

<span id="_pa"></span><span id="_PA"></span> **/pa**  
配置 SignTool 将验证指定的文件的数字签名*文件名*参数符合[PnP 设备安装签名要求](https://docs.microsoft.com/windows-hardware/drivers/install/pnp-device-installation-signing-requirements--windows-vista-and-later-)。

**请注意**  此选项不能用于**catdb**选项。

 

<span id="_pg__PolicyGUID"></span><span id="_pg__policyguid"></span><span id="_PG__POLICYGUID"></span> **/pg** *PolicyGUID*  
指定 guid 的验证策略。 PolicyGUID 对应于验证策略的 ActionID。

**请注意**  此选项不能用于**catdb**选项。

 

<span id="_ph__"></span><span id="_PH__"></span> **/ph**   
指定签名工具应打印并验证页面哈希值。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span> **/r** *RootSubjectName*  
指定签名证书必须链接到的根证书的使用者名称。 此值可以是根证书的整个主题名称的子字符串。

<span id="_tw"></span><span id="_TW"></span> **/tw**  
指定是否未对签名进行时间戳，则会生成一条警告。

### <a name="span-idgeneralswitchesspanspan-idgeneralswitchesspangeneral-options"></a><span id="general_switches"></span><span id="GENERAL_SWITCHES"></span>常规选项

<span id="_q"></span><span id="_Q"></span> **/q**  
配置 SignTool 将成功执行和失败的执行的最小输出上显示任何输出。

<span id="_v"></span><span id="_V"></span> **/v**  
配置 SignTool 将显示操作和警告消息的详细的版本。

<span id="__"></span> **/?**  
配置 SignTool 要在命令窗口中显示帮助信息。

<span id="FileName_..."></span><span id="filename_..."></span><span id="FILENAME_..."></span>*文件名...*  
指定一个或多个文件名称的列表。 具体取决于命令中，SignTool 将签名时间戳，或验证指定的文件。 如果**catdb**使用命令、 SignTool 将添加或从目录数据库中删除指定的文件。

有关**登录**，**时间戳**，并**验证**命令，文件可以是目录文件以[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)或驱动程序文件。

有关**catdb**命令时，文件必须为目录文件以[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

SignTool 支持大量的选项。 本主题中所述的选项仅限于那些可用于签名或验证驱动程序包或驱动程序文件。

SignTool 参数的完整列表，请参阅 Microsoft [SignTool](https://go.microsoft.com/fwlink/p/?linkid=62661)网站。

有关对文件进行签名的详细信息，请参阅 Microsoft[加密工具](https://go.microsoft.com/fwlink/p/?linkid=10637)网站。

SignTool 的 32 位版本位于 bin\\WDK 的 i386 文件夹。 该工具的 64 位版本位于 bin\\amd64 和 bin\\WDK 的 ia64 文件夹。

### <a name="span-idsigningexamplesspanspan-idsigningexamplesspansigning-examples"></a><span id="signing_examples"></span><span id="SIGNING_EXAMPLES"></span>签名示例

以下是如何进行签名的示例[驱动程序包的](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)使用软件发布者证书 (SPC) 和相应的交叉证书的目录文件。 此示例中是有效的签署驱动程序包的 64 位版本的 Windows Vista 和更高版本的 Windows，强制执行内核模式代码签名策略。 该示例对驱动程序包的目录文件 AbcCatFileName.cat 进行签名。 若要签名的编录文件，该示例使用交叉证书 AbcCrossCertificate 和 AbcSPCCertificate 证书。 AbcSPCCertificate 证书位于 AbcCertificateStore 证书存储中。

此示例还使用公开可用的时间戳服务器对目录文件进行签名。 时间戳服务器提供的 VeriSign 和其 URL 是 http://timestamp.verisign.com/scripts/timstamp.dll 。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.verisign.com/scripts/timstamp.dll AbcCatFileName.cat
```

下面是举例说明如何使用一个 SPC 和交叉证书的驱动程序文件中嵌入签名。 所有参数都是对进行签名的编录文件中，在这个例子相同只不过签名的文件而不是目录文件 AbcCatFileName.cat 是 AbcDriverFile.sys。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.verisign.com/scripts/timstamp.dll AbcDriverFile.sys
```

以下是如何进行签名的示例[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)文件中使用目录[商业版本发布证书](https://docs.microsoft.com/windows-hardware/drivers/install/commercial-release-certificate)或[商业测试证书](https://docs.microsoft.com/windows-hardware/drivers/install/commercial-test-certificate)。 此示例中是有效的 32 位版本的 Windows Vista 和更高版本的 Windows，不会强制使用内核模式代码签名策略驱动程序程序包进行签名。 该示例对驱动程序包的目录文件 CatalogFileName.cat 进行签名。 该示例使用 AbcTestCertificate 测试证书，位于 TestCertificateStore 证书存储区中，目录文件进行签名。

此示例还使用公开可用的时间戳服务器对目录文件进行签名。 时间戳服务器提供的 VeriSign 和其 URL 是 http://timestamp.verisign.com/scripts/timstamp.dll 。

```
SignTool sign /s TestCertificateStore /n AbcTestCertificate /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

### <a name="span-idverifyingexamplesspanspan-idverifyingexamplesspanverifying-examples"></a><span id="verifying_examples"></span><span id="VERIFYING_EXAMPLES"></span>验证示例

以下是举例说明如何验证签名[驱动程序包的](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)目录文件是否符合内核模式代码签名策略和即插即用设备安装签名要求。 该示例需要验证目录文件 AbcCatalogFile.cat 的签名。

```
SignTool verify /kp CatalogFileName.cat
```

下面是文件的举例说明如何验证签名的驱动程序包的目录文件中列出符合内核模式代码签名策略和即插即用设备安装签名要求。 该示例需要验证文件 AbcDriverPackage.inf，必须在目录文件 CatalogFileName.cat 中具有指纹条目的签名。

```
SignTool verify /kp /c CatalogFileName.cat AbcDriverPackage.inf
```

下面是如何进行验证的嵌入式的签名符合签名策略在 Windows Vista 和更高版本的 Windows 上的内核模式代码的示例。 该示例需要验证驱动程序文件 AbcDriverFile.sys 中嵌入的签名。

```
SignTool verify /kp AbcDriverFile.sys
```

以下是举例说明如何验证签名[驱动程序包的](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)目录文件是否符合即插即用设备安装签名要求。 该示例需要验证目录文件 CatalogFileName.cat 的签名。

```
SignTool verify /pa CatalogFileName.cat
```

### <a name="span-idexampleofaddingacatalogfiletothesystemcomponentdriverdataspanspan-idexampleofaddingacatalogfiletothesystemcomponentdriverdataspanexample-of-adding-a-catalog-file-to-the-system-component-driver-database"></a><span id="example_of_adding_a_catalog_file_to_the_system_component__driver__data"></span><span id="EXAMPLE_OF_ADDING_A_CATALOG_FILE_TO_THE_SYSTEM_COMPONENT__DRIVER__DATA"></span>添加到系统组件 （驱动程序） 数据库的目录文件的示例

下面是如何使用 SignTool 将目录文件 CatalogFileName.cat 添加到系统组件 （驱动程序） 数据库的示例。 **/V**选项配置 SignTool 将以详细模式运行并 **/u**选项配置 SignTool 生成要添加的目录文件的唯一名称，如有必要，以阻止替换具有与 CatalogFileName.cat 同名的现有目录文件。

```
SignTool catdb /v /u CatalogFileName.cat
```

 

 





