---
title: SignTool
description: 'SignTool ( # A0) 是一个命令行 CryptoAPI 工具，用于对文件进行数字签名，验证文件中的签名和时间戳文件。'
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
ms.openlocfilehash: 5aa4d58369226c97bc03e58f4feadcd667918d17
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716060"
---
# <a name="signtool"></a>SignTool

SignTool ( # A0) 是一个命令行 [CryptoAPI](/windows/win32/seccrypto/cryptography-portal) 工具，用于对文件进行数字签名，验证文件中的签名和时间戳文件。

```command
    SignTool [Operation] [Options] [FileName ...]
```

## <a name="partial-list-of-operations-options-and-arguments"></a>操作、选项和参数的部分列表

### <a name="operations"></a>Operations

**catdb**  
配置 SignTool 以更新目录数据库。 SignTool 可以将目录文件添加到数据库中，也可以从数据库中删除目录。 默认情况下， **catdb** 命令会将文件（其名称由 *FileName* 参数指定）添加到系统组件 (驱动程序) 数据库。

>[!NOTE]
>目录数据库用于自动查找目录文件。

**sign**  
将 SignTool 配置为使用 *FileName* 参数指定名称的文件进行数字签名。

**timestamp**  
将 SignTool 配置为使用 *FileName* 参数指定名称的文件的时间戳。

**verify**  
配置 SignTool 以验证其名称由 *FileName* 参数指定的文件的数字签名。

#### <a name="catdb-operation-options"></a>Catdb 操作选项

**/d**  
配置 SignTool 以更新目录数据库。 如果不使用 **/d** 和 **/g** 选项，则 SignTool 会更新系统组件和驱动程序数据库。

**/G** *Guid*  
配置 SignTool 以更新由 *GUID* 参数标识的目录数据库。

**/r**  
配置 SignTool 以从目录数据库中移除每个目录文件，其名称由 *FileName* 参数指定。 如果未指定此选项，SignTool 将向目录数据库添加指定的目录文件。

/u  
如有必要，配置 SignTool 以生成唯一名称，以防止与目录数据库中的现有目录文件发生冲突。 如果未指定此选项，SignTool 将覆盖与所添加的目录同名的任何现有目录。

#### <a name="sign-operation-options"></a>签名操作选项

**/a** 将 SignTool 配置为自动选择最佳签名证书。 如果此选项不存在，则 SignTool 会仅查找一个签名证书。

**/Ac** *CrossCertFileName*  
指定与软件发行者证书（ (SPC) 名为 " *CertificateName* " 并安装在证书存储 *StoreName*中的交叉证书文件的名称。 仅当签名证书为 SPC 时，才应使用此选项。

**/c** *CertTemplateName*  
指定用于对证书进行签名的证书模板名（一个 Microsoft 扩展）。

**/Csp** *CSPName*  
指定包含私钥容器的加密服务提供程序 (CSP)。

**/D** *Desc*  
指定已签名内容的说明。

**/Du** *URL*  
指定已签名内容的展开说明的 URL。

**/F** *SignCertFile*  
指定文件中的签名证书。 仅支持 (PFX) 文件格式的个人信息交换。 可以使用 [**Pvk2Pfx**](pvk2pfx.md) 工具将 SPC 和 PVK 文件转换为 PFX 格式。

如果该文件是使用密码保护的 PFX 格式，则使用 **/p** 选项来指定密码。 如果文件不包含私钥，请分别使用 **/csp** 和 **/k** 选项来指定 csp 和私钥容器名称。

**/fd**  
指定要用于创建文件签名的文件摘要算法。 默认值为 SHA1。

**/I** *IssuerName*  
指定签名证书的颁发者的名称。 该值可以是整个颁发者名称的子字符串。

**/J** *DLL*  
指定提供签名特性的 DLL 的名称。

**/Jp** *ParameterName*  
指定传递给 **/j** 命令指定的 DLL 的参数。

**/Kc** *PrivKeyContainerName*  
指定私钥的密钥容器名称。

**/N** *SubjectName*  
指定签名证书的主题的名称。 该值可以是整个主题名称的子字符串。

**/nph**  
如果支持，则取消可执行文件的页面哈希。 默认值由 SIGNTOOL \_ 页面 \_ 哈希环境变量和 wintrust.dll 版本确定。 对于非 PE 文件，忽略此选项。

**/P** *密码*  
指定打开 PFX 文件时要使用的密码。 PFX 文件可以使用 **/f** 选项指定

**/P7** *路径*  
指定为每个指定的内容文件生成的公钥加密标准 (PKCS) \# 7 文件。 PKCS \# 7 文件命名为 \\ p7。

**/P7ce** *值*  
指定已签名的 PKCS \# 7 内容的选项。 将 "值" 设置为 "Embedded" 以将签名内容嵌入 PKCS \# 7 文件中，或设置为 "DetachedSignedData" 以生成已分离的 pkcs 7 文件的已签名数据部分 \# 。 如果未使用 **/p7ce** 选项，则默认情况下将嵌入已签名的内容。

**/P7co** *OID*  
指定标识已签名的 PKCS 7 内容 (OID) 的对象标识符 \# 。

**/ph 在** 如果支持，则生成可执行文件的页面哈希。

**/R** *RootSubjectName*  
指定签名证书必须链接到的根证书的使用者名称。 该值可以是根证书的整个主题名称的子字符串。

**/S** *StoreName*  
指定在搜索要用于对文件进行签名的证书时要打开的证书存储区的名称。 如果未指定此选项，则打开 " **我** 的证书存储区"。

**/Sha1** *哈希*  
指定签名证书的 SHA1 哈希。

**/sm**  
将 SignTool 配置为使用计算机证书存储而不是用户证书存储区。

**/T** *URL*  
指定时间戳服务器的 URL。 如果未提供此选项，则签名文件不是时间戳。 目录文件或驱动程序文件应带有时间戳，因为如果签名者的密钥已泄露，则时间戳将提供吊销用于对文件进行签名的密钥所需的信息。

**/td** *alg*  
与/tr 选项一起使用，以请求 RFC 3161 时间戳服务器使用的摘要算法。

**/Tr** *URL*  
指定 RFC 3161 时间戳服务器的 URL。 如果此选项 (或 **/t**) 不存在，则将不会对签名的文件加盖时间戳。 如果时间戳操作失败，将生成一个警告。 此选项不能与 **/t** 选项一起使用。

**/U** *用法*  
指定签名证书中必须存在的增强型密钥用法 (EKU)。 可以通过 OID 或字符串指定该用法的值。 默认用法为“代码签名”(1.3.6.1.5.5.7.3.3)。

**/uw** 指定 (1.3.6.1.4.1.311.10.3.6) 使用 "Windows 系统组件验证"。

#### <a name="timestamp-operation-options"></a>时间戳操作选项

**/p7** 时间戳 PKCS \# 7 文件。

**/T** *URL*  
指定时间戳服务器的 URL。 必须事先签署带有时间戳的文件

**/td** *alg*  
请求 RFC 3161 时间戳服务器使用的摘要算法。 **/td** 与 **/tr** 选项一起使用。

**/tp** *索引*  
对引用处的签名进行时间戳操作。

**/tr** *alg*  
请求 RFC 3161 时间戳服务器使用的摘要算法。 **/td** 与 **/tr** 选项一起使用。

#### <a name="verify-operation-options"></a>验证操作选项

**/a**  
指定可以使用所有方法来验证文件。 首先，搜索目录数据库以确定是否在目录中对文件进行签名。 如果未在任何目录中对文件进行签名，SignTool 会尝试验证文件的嵌入签名。 验证可以或不能在目录中进行签名的文件时，建议使用该选项。

**/ad**  
指定仅在默认目录数据库中搜索该文件已登录的目录。

**/all**  
验证包含多个签名的文件中的所有签名。

**/as**  
指定仅在系统组件 (驱动程序) 目录数据库中搜索该文件登录到的目录。

**/Ag** *由 catdbguid*  
指定仅在通过 *由 catdbguid* 参数标识的目录数据库中搜索该文件已登录的目录。

**/c** *CatalogFileName*  
指定编录文件的名称。

**/d** 指定签名工具应打印描述和描述 URL。

**/ds** *索引*  
验证指定位置的签名。

**/hash** {**SHA1** | **SHA256**}  
指定在目录中搜索文件时要使用的可选哈希算法。

**/kp**  
配置 SignTool 以验证 *FileName* 参数指定的每个文件的数字签名是否符合 [内核模式代码签名策略](../install/kernel-mode-code-signing-policy--windows-vista-and-later-.md) 和 windows Vista 和更高版本的 windows Vista 的 [PnP 设备安装签名要求](../install/pnp-device-installation-signing-requirements--windows-vista-and-later-.md) 。 如果未指定此选项，则 SignTool 仅验证签名是否符合 PnP 设备安装签名要求。

**/ms**  
使用多个验证语义。 这是 Windows 8 及更高版本上的 [**WinVerifyTrust 函数**](/windows/win32/api/wintrust/nf-wintrust-winverifytrust) 调用的默认行为。

**/O** *版本*  
按操作系统版本验证文件。 *版本*参数的格式为*PlatformID： VerMajor. VerMinor. BuildNumber*

建议使用 **/o** 选项。 如果未指定 **/o** ，SignTool 可能会返回意外的结果。 例如，如果不包含 **/o** 选项，则在较早的操作系统上正确验证的系统目录可能无法在较新的操作系统上正确验证。

**/p7**  
验证 PKCS \# 7 文件。 无现有策略用于 PKCS \# 7 验证。 该签名处于选中状态，并为签名证书生成了链。

**/pa**  
配置 SignTool，以验证 *FileName* 参数指定的每个文件的数字签名是否符合 [PnP 设备安装签名要求](../install/pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

>[!NOTE]
>此选项不能与 **catdb** 选项一起使用。

**/Pg** *PolicyGUID*  
通过 GUID 指定验证策略。 PolicyGUID 对应于验证策略的 ActionID。

>[!NOTE]
>此选项不能与 **catdb** 选项一起使用。

**/ph 在** 指定签名工具应打印并验证页面哈希值。

**/R** *RootSubjectName*  
指定签名证书必须链接到的根证书的使用者名称。 该值可以是根证书的整个主题名称的子字符串。

**/tw**  
如果签名没有时间戳，则指定生成警告。

### <a name="general-options"></a>常规选项

**/q**  
配置 SignTool 以在成功执行时不显示输出，并将最小输出配置为失败的执行。

**/v**  
配置 SignTool 以显示操作和警告消息的详细版本。

**/?**  
配置 SignTool 以在命令窗口中显示帮助信息。

*FileName .。。*  
指定一个或多个文件名的列表。 根据命令，SignTool 将对指定的文件进行签名、时间戳或验证。 如果使用 **catdb** 命令，SignTool 将在目录数据库中添加或删除指定的文件。

对于 **sign**、 **timestamp**和 **verify** 命令，文件可以是 [驱动程序包](../install/driver-packages.md) 或驱动程序文件的目录文件。

对于 **catdb** 命令，文件必须是 [驱动程序包](../install/driver-packages.md)的编录文件。

## <a name="remarks"></a>备注

SignTool 支持大量选项。 本主题中所述的选项仅限于可用于对驱动程序包或驱动程序文件进行签名或验证的选项。

有关 SignTool 参数的完整列表，请参阅 Microsoft [SignTool](/windows/win32/seccrypto/signtool) 网站。

有关签名文件的详细信息，请参阅 Microsoft [加密工具](/windows/win32/seccrypto/cryptography-tools) 网站。

SignTool 的32位版本位于 WDK 的 "bin" \\ 文件夹中。 此工具的64位版本位于 WDK 的 bin \\ 和 bin \\ ia64 文件夹中。

## <a name="examples"></a>示例

下面的示例演示如何使用软件发行者证书 (SPC) 和相应的交叉证书对 [驱动程序包的](../install/driver-packages.md) 目录文件进行签名。 此示例适用于对64位版本的 Windows Vista 和更高版本的 Windows 的驱动程序包进行签名，这将强制实施内核模式代码签名策略。 该示例对驱动程序包的目录文件 AbcCatFileName.cat 进行签名。 若要对编录文件进行签名，该示例使用了交叉证书 AbcCrossCertificate 和 AbcSPCCertificate 证书。 AbcSPCCertificate 证书位于 AbcCertificateStore 证书存储区中。

该示例还使用公开提供的时间戳服务器对目录文件进行签名。 时间戳服务器由 DigiCert 提供，其 URL 为 `http://timestamp.digicert.com` 。

```command
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.digicert.com AbcCatFileName.cat
```

下面的示例演示如何使用 SPC 和交叉证书将签名嵌入驱动程序文件。 所有参数与签署目录文件的示例中的参数相同，不同之处在于签名的文件是 AbcDriverFile.sys 而不是编录文件 AbcCatFileName.cat。

```command
SignTool sign /ac AbcCrossCertificate.cer /s AbcCertificateStore /n AbcSPCCertificate /t http://timestamp.digicert.com AbcDriverFile.sys
```

下面的示例演示如何使用[商业发布证书](../install/commercial-release-certificate.md)或[商业测试证书](../install/commercial-test-certificate.md)对[驱动程序包的](../install/driver-packages.md)目录文件进行签名。 此示例适用于对32位版本的 Windows Vista 和更高版本的 Windows 的驱动程序包进行签名，这不会强制实施内核模式代码签名策略。 该示例对驱动程序包的目录文件 CatalogFileName.cat 进行签名。 该示例使用位于 TestCertificateStore 证书存储区中的 AbcTestCertificate 测试证书对编录文件进行签名。

该示例还使用公开提供的时间戳服务器对目录文件进行签名。 时间戳服务器由 DigiCert 提供，其 URL 为 `http://timestamp.digicert.com` 。

```command
SignTool sign /s TestCertificateStore /n AbcTestCertificate /t http://timestamp.digicert.com CatalogFileName.cat
```

### <a name="verifying-examples"></a>验证示例

下面的示例演示如何验证 [驱动程序包](../install/driver-packages.md) 的目录文件的签名是否符合内核模式代码签名策略和 PnP 设备安装签名要求。 该示例将验证目录文件 AbcCatalogFile.cat 的签名。

```command
SignTool verify /kp CatalogFileName.cat
```

下面的示例演示如何验证驱动程序包的目录文件中列出的文件的签名是否符合内核模式代码签名策略和 PnP 设备安装签名要求。 该示例验证文件 AbcDriverPackage 的签名，该文件必须在目录文件 CatalogFileName.cat 中具有指纹条目。

```command
SignTool verify /kp /c CatalogFileName.cat AbcDriverPackage.inf
```

下面的示例演示如何验证嵌入的签名是否符合 Windows Vista 和更高版本的 Windows 上的内核模式代码签名策略。 该示例验证 AbcDriverFile.sys 中嵌入的驱动程序文件中的签名。

```command
SignTool verify /kp AbcDriverFile.sys
```

下面的示例演示如何验证 [驱动程序包](../install/driver-packages.md) 的目录文件的签名是否符合 PnP 设备安装签名要求。 该示例将验证目录文件 CatalogFileName.cat 的签名。

```command
SignTool verify /pa CatalogFileName.cat
```

### <a name="example-of-adding-a-catalog-file-to-the-system-component-driver-database"></a>将目录文件添加到系统组件的示例 (驱动程序) 数据库

下面的示例演示如何使用 SignTool 将目录文件 CatalogFileName.cat 添加到系统组件 (驱动程序) 数据库。 **/V**选项将 SignTool 配置为在详细模式下操作，而 **/U**选项将 SignTool 配置为为所添加的目录文件生成唯一名称（如有必要），以防止替换现有的同名目录文件，该文件与 CatalogFileName.cat 相同。

```command
SignTool catdb /v /u CatalogFileName.cat
```