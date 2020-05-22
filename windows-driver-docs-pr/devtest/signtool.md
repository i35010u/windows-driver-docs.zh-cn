---
title: SignTool
description: SignTool （Signtool）是一种命令行 CryptoAPI 工具，用于对文件进行数字签名，验证文件中的签名和时间戳文件。
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
ms.openlocfilehash: 491e1f8214fe2caca701472c2fa9baf2f7e45194
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769673"
---
# <a name="signtool"></a>SignTool


SignTool （Signtool）是一种命令行[CryptoAPI](https://docs.microsoft.com/windows/win32/seccrypto/cryptography-portal)工具，用于对文件进行数字签名，验证文件中的签名和时间戳文件。

```
    SignTool [Operation] [Options] [FileName ...]
```

### <a name="span-idpartial_list_of_operations__switches__and_argumentsspanspan-idpartial_list_of_operations__switches__and_argumentsspanpartial-list-of-operations-options-and-arguments"></a><span id="partial_list_of_operations__switches__and_arguments"></span><span id="PARTIAL_LIST_OF_OPERATIONS__SWITCHES__AND_ARGUMENTS"></span>操作、选项和参数的部分列表

### <a name="span-idoperationsspanspan-idoperationsspanoperations"></a><span id="operations"></span><span id="OPERATIONS"></span>运算符

<span id="catdb"></span><span id="CATDB"></span>**catdb**  
配置 SignTool 以更新目录数据库。 SignTool 可以将目录文件添加到数据库中，也可以从数据库中删除目录。 默认情况下， **catdb**命令会将文件（其名称由*FileName*参数指定）添加到系统组件（驱动程序）数据库中。

**注意**   目录数据库用于自动查找目录文件。

 

<span id="sign"></span><span id="SIGN"></span>**表明**  
将 SignTool 配置为使用*FileName*参数指定名称的文件进行数字签名。

<span id="timestamp"></span><span id="TIMESTAMP"></span>**标志**  
将 SignTool 配置为使用*FileName*参数指定名称的文件的时间戳。

<span id="verify"></span><span id="VERIFY"></span>**}**  
配置 SignTool 以验证其名称由*FileName*参数指定的文件的数字签名。

### <a name="span-idcatdb_operation_switchesspanspan-idcatdb_operation_switchesspancatdb-operation-options"></a><span id="catdb_operation_switches"></span><span id="CATDB_OPERATION_SWITCHES"></span>Catdb 操作选项

<span id="_d"></span><span id="_D"></span>**/d**  
配置 SignTool 以更新目录数据库。 如果不使用 **/d**和 **/g**选项，则 SignTool 会更新系统组件和驱动程序数据库。

<span id="_g_Guid"></span><span id="_g_guid"></span><span id="_G_GUID"></span>**/G** *Guid*  
配置 SignTool 以更新由*GUID*参数标识的目录数据库。

<span id="_r"></span><span id="_R"></span>**/r**  
配置 SignTool 以从目录数据库中移除每个目录文件，其名称由*FileName*参数指定。 如果未指定此选项，SignTool 将向目录数据库添加指定的目录文件。

<span id="_u"></span><span id="_U"></span>**/u**  
如有必要，配置 SignTool 以生成唯一名称，以防止与目录数据库中的现有目录文件发生冲突。 如果未指定此选项，SignTool 将覆盖与所添加的目录同名的任何现有目录。

### <a name="span-idsign_operation_switchesspanspan-idsign_operation_switchesspansign-operation-options"></a><span id="sign_operation_switches"></span><span id="SIGN_OPERATION_SWITCHES"></span>签名操作选项

<span id="_a_"></span><span id="_A_"></span>**/a**   
将 SignTool 配置为自动选择最佳签名证书。 如果此选项不存在，则 SignTool 会仅查找一个签名证书。

<span id="_ac_CrossCertFileName"></span><span id="_ac_crosscertfilename"></span><span id="_AC_CROSSCERTFILENAME"></span>**/Ac** *CrossCertFileName*  
指定与软件发行者证书（SPC）（名为*CertificateName* ）一起使用的交叉证书文件的名称，并将其安装在证书存储*StoreName*中。 仅当签名证书为 SPC 时，才应使用此选项。

<span id="_c_CertTemplateName"></span><span id="_c_certtemplatename"></span><span id="_C_CERTTEMPLATENAME"></span>**/c** *CertTemplateName*  
指定用于对证书进行签名的证书模板名（一个 Microsoft 扩展）。

<span id="_csp_CSPName"></span><span id="_csp_cspname"></span><span id="_CSP_CSPNAME"></span>**/Csp** *CSPName*  
指定包含私钥容器的加密服务提供程序 (CSP)。

<span id="_d_Desc"></span><span id="_d_desc"></span><span id="_D_DESC"></span>**/D** *Desc*  
指定已签名内容的说明。

<span id="_du_URL"></span><span id="_du_url"></span><span id="_DU_URL"></span>**/Du** *URL*  
指定已签名内容的展开说明的 URL。

<span id="_f_SignCertFile"></span><span id="_f_signcertfile"></span><span id="_F_SIGNCERTFILE"></span>**/F** *SignCertFile*  
指定文件中的签名证书。 仅支持个人信息交换（PFX）文件格式。 可以使用[**Pvk2Pfx**](pvk2pfx.md)工具将 SPC 和 PVK 文件转换为 PFX 格式。

如果该文件是使用密码保护的 PFX 格式，则使用 **/p**选项来指定密码。 如果文件不包含私钥，请分别使用 **/csp**和 **/k**选项来指定 csp 和私钥容器名称。

<span id="_fd"></span><span id="_FD"></span>**/fd**  
指定要用于创建文件签名的文件摘要算法。 默认值为 SHA1。

<span id="_i_IssuerName"></span><span id="_i_issuername"></span><span id="_I_ISSUERNAME"></span>**/I** *IssuerName*  
指定签名证书的颁发者的名称。 该值可以是整个颁发者名称的子字符串。

<span id="_j_DLL"></span><span id="_j_dll"></span><span id="_J_DLL"></span>**/J** *DLL*  
指定提供签名特性的 DLL 的名称。

<span id="_jp_ParameterName"></span><span id="_jp_parametername"></span><span id="_JP_PARAMETERNAME"></span>**/Jp** *ParameterName*  
指定传递给 **/j**命令指定的 DLL 的参数。

<span id="_kc_PrivKeyContainerName"></span><span id="_kc_privkeycontainername"></span><span id="_KC_PRIVKEYCONTAINERNAME"></span>**/Kc** *PrivKeyContainerName*  
指定私钥的密钥容器名称。

<span id="_n_SubjectName"></span><span id="_n_subjectname"></span><span id="_N_SUBJECTNAME"></span>**/N** *SubjectName*  
指定签名证书的主题的名称。 该值可以是整个主题名称的子字符串。

<span id="_nph"></span><span id="_NPH"></span>**/nph**  
如果支持，则取消可执行文件的页面哈希。 默认值由 SIGNTOOL \_ 页面 \_ 哈希环境变量和 wintrust.dll 版本确定。 对于非 PE 文件，忽略此选项。

<span id="_p_Password"></span><span id="_p_password"></span><span id="_P_PASSWORD"></span>**/P** *密码*  
指定打开 PFX 文件时要使用的密码。 PFX 文件可以使用 **/f**选项指定

<span id="_p7__Path"></span><span id="_p7__path"></span><span id="_P7__PATH"></span>**/P7** *路径*  
指定为 \# 每个指定的内容文件生成公钥加密标准（PKCS）7文件。 PKCS \# 7 文件命名为 \\ p7。

<span id="_p7ce_Value"></span><span id="_p7ce_value"></span><span id="_P7CE_VALUE"></span>**/P7ce** *值*  
指定已签名的 PKCS \# 7 内容的选项。 将 "值" 设置为 "Embedded" 以将签名内容嵌入 PKCS \# 7 文件中，或设置为 "DetachedSignedData" 以生成已分离的 pkcs 7 文件的已签名数据部分 \# 。 如果未使用 **/p7ce**选项，则默认情况下将嵌入已签名的内容。

<span id="_p7co__OID"></span><span id="_p7co__oid"></span><span id="_P7CO__OID"></span>**/P7co** *OID*  
指定标识已签名的 PKCS 7 内容的对象标识符（OID） \# 。

<span id="_ph___"></span><span id="_PH___"></span>**/ph 在**   
如果支持，则生成可执行文件的页面哈希。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span>**/R** *RootSubjectName*  
指定签名证书必须链接到的根证书的使用者名称。 该值可以是根证书的整个主题名称的子字符串。

<span id="_s_StoreName"></span><span id="_s_storename"></span><span id="_S_STORENAME"></span>**/S** *StoreName*  
指定在搜索要用于对文件进行签名的证书时要打开的证书存储区的名称。 如果未指定此选项，则打开 "**我**的证书存储区"。

<span id="_sha1_Hash"></span><span id="_sha1_hash"></span><span id="_SHA1_HASH"></span>**/Sha1** *哈希*  
指定签名证书的 SHA1 哈希。

<span id="_sm"></span><span id="_SM"></span>**/sm**  
将 SignTool 配置为使用计算机证书存储而不是用户证书存储区。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span>**/T** *URL*  
指定时间戳服务器的 URL。 如果未提供此选项，则签名文件不是时间戳。 目录文件或驱动程序文件应带有时间戳，因为如果签名者的密钥已泄露，则时间戳将提供吊销用于对文件进行签名的密钥所需的信息。

<span id="_td____alg"></span><span id="_TD____ALG"></span>**/td** *alg*  
与/tr 选项一起使用，以请求 RFC 3161 时间戳服务器使用的摘要算法。

<span id="_tr___URL"></span><span id="_tr___url"></span><span id="_TR___URL"></span>**/Tr** *URL*  
指定 RFC 3161 时间戳服务器的 URL。 如果该选项（或 **/t**）不存在，则不会对签名的文件加盖时间戳。 如果时间戳操作失败，将生成一个警告。 此选项不能与 **/t**选项一起使用。

<span id="_u___Usage"></span><span id="_u___usage"></span><span id="_U___USAGE"></span>**/U** *用法*  
指定签名证书中必须存在的增强型密钥用法 (EKU)。 可以通过 OID 或字符串指定该用法的值。 默认用法为“代码签名”(1.3.6.1.5.5.7.3.3)。

<span id="_uw_"></span><span id="_UW_"></span>**/uw**   
指定“Windows 系统组件验证”(1.3.6.1.4.1.311.10.3.6) 的用法。

### <a name="span-idtimestamp_operation_switchesspanspan-idtimestamp_operation_switchesspantimestamp-operation-options"></a><span id="timestamp_operation_switches"></span><span id="TIMESTAMP_OPERATION_SWITCHES"></span>时间戳操作选项

<span id="_p7_"></span><span id="_P7_"></span>**/p7**   
时间戳 PKCS \# 7 文件。

<span id="_t_URL"></span><span id="_t_url"></span><span id="_T_URL"></span>**/T** *URL*  
指定时间戳服务器的 URL。 必须事先签署带有时间戳的文件

<span id="_td___alg"></span><span id="_TD___ALG"></span>**/td** *alg*  
请求 RFC 3161 时间戳服务器使用的摘要算法。 **/td**与 **/tr**选项一起使用。

<span id="_tp__index"></span><span id="_TP__INDEX"></span>**/tp** *索引*  
对引用处的签名进行时间戳操作。

<span id="_tr___alg"></span><span id="_TR___ALG"></span>**/tr** *alg*  
请求 RFC 3161 时间戳服务器使用的摘要算法。 **/td**与 **/tr**选项一起使用。

### <a name="span-idverify_operation_switchesspanspan-idverify_operation_switchesspanverify-operation-options"></a><span id="verify_operation_switches"></span><span id="VERIFY_OPERATION_SWITCHES"></span>验证操作选项

<span id="_a"></span><span id="_A"></span>**/a**  
指定可以使用所有方法来验证文件。 首先，搜索目录数据库以确定是否在目录中对文件进行签名。 如果未在任何目录中对文件进行签名，SignTool 会尝试验证文件的嵌入签名。 验证可以或不能在目录中进行签名的文件时，建议使用该选项。

<span id="_ad"></span><span id="_AD"></span>**/ad**  
指定仅在默认目录数据库中搜索该文件已登录的目录。

<span id="_all"></span><span id="_ALL"></span>**/all**  
验证包含多个签名的文件中的所有签名。

<span id="_as"></span><span id="_AS"></span>**/as**  
指定仅在系统组件（驱动程序）目录数据库中搜索该文件已登录的目录。

<span id="_ag_CatDBGUID"></span><span id="_ag_catdbguid"></span><span id="_AG_CATDBGUID"></span>**/Ag** *由 catdbguid*  
指定仅在通过*由 catdbguid*参数标识的目录数据库中搜索该文件已登录的目录。

<span id="_c___CatalogFileName"></span><span id="_c___catalogfilename"></span><span id="_C___CATALOGFILENAME"></span>**/c** *CatalogFileName*  
指定编录文件的名称。

<span id="_d___"></span><span id="_D___"></span>**/d**   
指定签名工具应打印描述和描述 URL。

<span id="_ds___index"></span><span id="_DS___INDEX"></span>**/ds** *索引*  
验证指定位置的签名。

<span id="_hash__SHA1SHA256"></span><span id="_hash__sha1sha256"></span><span id="_HASH__SHA1SHA256"></span>**/hash** {**SHA1** | **SHA256**}  
指定在目录中搜索文件时要使用的可选哈希算法。

<span id="_kp"></span><span id="_KP"></span>**/kp**  
配置 SignTool 以验证*FileName*参数指定的每个文件的数字签名是否符合[内核模式代码签名策略](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-policy--windows-vista-and-later-)和 windows Vista 和更高版本的 windows Vista 的[PnP 设备安装签名要求](https://docs.microsoft.com/windows-hardware/drivers/install/pnp-device-installation-signing-requirements--windows-vista-and-later-)。 如果未指定此选项，则 SignTool 仅验证签名是否符合 PnP 设备安装签名要求。

<span id="_ms"></span><span id="_MS"></span>**/ms**  
使用多个验证语义。 这是 Windows 8 及更高版本上的[**WinVerifyTrust 函数**](https://docs.microsoft.com/windows/desktop/api/wintrust/nf-wintrust-winverifytrust)调用的默认行为。

<span id="_o_Version"></span><span id="_o_version"></span><span id="_O_VERSION"></span>**/O** *版本*  
按操作系统版本验证文件。 *版本*参数的格式为<em>PlatformID</em>**：**<em>VerMajor</em>**。**<em>VerMinor</em>**。**<em>BuildNumber</em>

建议使用 **/o**选项。 如果未指定 **/o** ，SignTool 可能会返回意外的结果。 例如，如果不包含 **/o**选项，则在较早的操作系统上正确验证的系统目录可能无法在较新的操作系统上正确验证。

<span id="_p7"></span><span id="_P7"></span>**/p7**  
验证 PKCS \# 7 文件。 无现有策略用于 PKCS \# 7 验证。 该签名处于选中状态，并为签名证书生成了链。

<span id="_pa"></span><span id="_PA"></span>**/pa**  
配置 SignTool，以验证*FileName*参数指定的每个文件的数字签名是否符合[PnP 设备安装签名要求](https://docs.microsoft.com/windows-hardware/drivers/install/pnp-device-installation-signing-requirements--windows-vista-and-later-)。

**注意**   此选项不能与**catdb**选项一起使用。

 

<span id="_pg__PolicyGUID"></span><span id="_pg__policyguid"></span><span id="_PG__POLICYGUID"></span>**/Pg** *PolicyGUID*  
通过 GUID 指定验证策略。 PolicyGUID 对应于验证策略的 ActionID。

**注意**   此选项不能与**catdb**选项一起使用。

 

<span id="_ph__"></span><span id="_PH__"></span>**/ph 在**   
指定签名工具应打印并验证页面哈希值。

<span id="_r_RootSubjectName"></span><span id="_r_rootsubjectname"></span><span id="_R_ROOTSUBJECTNAME"></span>**/R** *RootSubjectName*  
指定签名证书必须链接到的根证书的使用者名称。 该值可以是根证书的整个主题名称的子字符串。

<span id="_tw"></span><span id="_TW"></span>**/tw**  
如果签名没有时间戳，则指定生成警告。

### <a name="span-idgeneral_switchesspanspan-idgeneral_switchesspangeneral-options"></a><span id="general_switches"></span><span id="GENERAL_SWITCHES"></span>常规选项

<span id="_q"></span><span id="_Q"></span>**/q**  
配置 SignTool 以在成功执行时不显示输出，并将最小输出配置为失败的执行。

<span id="_v"></span><span id="_V"></span>**/v**  
配置 SignTool 以显示操作和警告消息的详细版本。

<span id="__"></span>**/?**  
配置 SignTool 以在命令窗口中显示帮助信息。

<span id="FileName_..."></span><span id="filename_..."></span><span id="FILENAME_..."></span>*FileName .。。*  
指定一个或多个文件名的列表。 根据命令，SignTool 将对指定的文件进行签名、时间戳或验证。 如果使用**catdb**命令，SignTool 将在目录数据库中添加或删除指定的文件。

对于**sign**、 **timestamp**和**verify**命令，文件可以是[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)或驱动程序文件的目录文件。

对于**catdb**命令，文件必须是[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)的编录文件。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

SignTool 支持大量选项。 本主题中所述的选项仅限于可用于对驱动程序包或驱动程序文件进行签名或验证的选项。

有关 SignTool 参数的完整列表，请参阅 Microsoft [SignTool](https://docs.microsoft.com/windows/win32/seccrypto/signtool)网站。

有关签名文件的详细信息，请参阅 Microsoft[加密工具](https://docs.microsoft.com/windows/win32/seccrypto/cryptography-tools)网站。

SignTool 的32位版本位于 WDK 的 "bin" \\ 文件夹中。 此工具的64位版本位于 WDK 的 bin \\ 和 bin \\ ia64 文件夹中。

### <a name="span-idsigning_examplesspanspan-idsigning_examplesspansigning-examples"></a><span id="signing_examples"></span><span id="SIGNING_EXAMPLES"></span>签名示例

下面的示例演示如何使用软件发行者证书（SPC）和相应的交叉证书对[驱动程序包的](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)目录文件进行签名。 此示例适用于对64位版本的 Windows Vista 和更高版本的 Windows 的驱动程序包进行签名，这将强制实施内核模式代码签名策略。 该示例对驱动程序包的目录文件 AbcCatFileName.cat 进行签名。 若要对编录文件进行签名，该示例使用了交叉证书 AbcCrossCertificate 和 AbcSPCCertificate 证书。 AbcSPCCertificate 证书位于 AbcCertificateStore 证书存储区中。

该示例还使用公开提供的时间戳服务器对目录文件进行签名。 时间戳服务器由 DigiCert 提供，其 URL 为 http://timestamp.digicert.com 。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.digicert.com AbcCatFileName.cat
```

下面的示例演示如何使用 SPC 和交叉证书将签名嵌入驱动程序文件。 所有参数与签署目录文件的示例中的参数相同，不同之处在于签名的文件是 AbcDriverFile 而不是编录文件 AbcCatFileName.cat。

```
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.digicert.com AbcDriverFile.sys
```

下面的示例演示如何使用[商业发布证书](https://docs.microsoft.com/windows-hardware/drivers/install/commercial-release-certificate)或[商业测试证书](https://docs.microsoft.com/windows-hardware/drivers/install/commercial-test-certificate)对[驱动程序包的](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)目录文件进行签名。 此示例适用于对32位版本的 Windows Vista 和更高版本的 Windows 的驱动程序包进行签名，这不会强制实施内核模式代码签名策略。 该示例对驱动程序包的目录文件 CatalogFileName.cat 进行签名。 该示例使用位于 TestCertificateStore 证书存储区中的 AbcTestCertificate 测试证书对编录文件进行签名。

该示例还使用公开提供的时间戳服务器对目录文件进行签名。 时间戳服务器由 DigiCert 提供，其 URL 为 http://timestamp.digicert.com 。

```
SignTool sign /s TestCertificateStore /n AbcTestCertificate /t http://timestamp.digicert.com CatalogFileName.cat
```

### <a name="span-idverifying_examplesspanspan-idverifying_examplesspanverifying-examples"></a><span id="verifying_examples"></span><span id="VERIFYING_EXAMPLES"></span>验证示例

下面的示例演示如何验证[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)的目录文件的签名是否符合内核模式代码签名策略和 PnP 设备安装签名要求。 该示例将验证目录文件 AbcCatalogFile.cat 的签名。

```
SignTool verify /kp CatalogFileName.cat
```

下面的示例演示如何验证驱动程序包的目录文件中列出的文件的签名是否符合内核模式代码签名策略和 PnP 设备安装签名要求。 该示例验证文件 AbcDriverPackage 的签名，该文件必须在目录文件 CatalogFileName.cat 中具有指纹条目。

```
SignTool verify /kp /c CatalogFileName.cat AbcDriverPackage.inf
```

下面的示例演示如何验证嵌入的签名是否符合 Windows Vista 和更高版本的 Windows 上的内核模式代码签名策略。 该示例将验证嵌入驱动程序文件 AbcDriverFile 中的签名。

```
SignTool verify /kp AbcDriverFile.sys
```

下面的示例演示如何验证[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)的目录文件的签名是否符合 PnP 设备安装签名要求。 该示例将验证目录文件 CatalogFileName.cat 的签名。

```
SignTool verify /pa CatalogFileName.cat
```

### <a name="span-idexample_of_adding_a_catalog_file_to_the_system_component__driver__dataspanspan-idexample_of_adding_a_catalog_file_to_the_system_component__driver__dataspanexample-of-adding-a-catalog-file-to-the-system-component-driver-database"></a><span id="example_of_adding_a_catalog_file_to_the_system_component__driver__data"></span><span id="EXAMPLE_OF_ADDING_A_CATALOG_FILE_TO_THE_SYSTEM_COMPONENT__DRIVER__DATA"></span>将目录文件添加到系统组件（驱动程序）数据库的示例

下面的示例演示如何使用 SignTool 将目录文件 CatalogFileName.cat 添加到系统组件（驱动程序）数据库中。 **/V**选项将 SignTool 配置为在详细模式下操作，而 **/U**选项将 SignTool 配置为为所添加的目录文件生成唯一名称（如有必要），以防止替换现有的同名目录文件，该文件与 CatalogFileName.cat 相同。

```
SignTool catdb /v /u CatalogFileName.cat
```

 

 





