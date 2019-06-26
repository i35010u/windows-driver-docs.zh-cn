---
title: 发布签名
description: 完成测试签名和验证该驱动程序已准备好发布后，驱动程序包必须是已签名的版本。 有两种方法的签名的驱动程序包的版本。
ms.assetid: 71499A0A-95D0-411C-84D1-C4B91FA4E6B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84bc3d2439fbc48fe552372fa6928da5128389b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387316"
---
# <a name="release-signing"></a>发布签名


完成测试签名和验证该驱动程序已准备好发布后，驱动程序包必须是已签名的版本。 有两种方法的签名的驱动程序包的版本。

版本签名标识将加载到 Windows Vista 内核模式或用户模式下的二进制文件 （例如，.sys 或.dll 文件） 的发布者和更高版本的 Windows。

内核模式二进制文件是通过已发布签名：

1.  Windows 硬件质量实验室 (WHQL 也称为 Winqual) 以释放签署驱动程序包。 WHQL 版本签名是通过 Windows 认证计划获得的。 以下链接介绍从开始到结束 Windows 认证计划上的五个步骤。 请参阅[Windows 硬件认证： 从这里开始](https://docs.microsoft.com/previous-versions/hh833792(v=msdn.10))有关此选项的详细信息。 在上面的链接中的步骤的任何问题应会定向到<sysdev@microsft.com>别名。
2.  而不是使用 WHQL 程序，驱动程序包可以是由驱动程序开发人员和供应商签名的版本。 此程序已开始从 Vista OS 版本。 版本签名会创建通过软件发行者证书 (SPC)。 从 Microsoft 授权颁发此类证书的第三方证书颁发机构 (CA) 获取 SPC。 使用这种类型的 SPC 生成的签名也符合 64 位和 32 位版本的 Windows Vista 和更高版本的 Windows 的即插即用驱动程序签名要求

接下来介绍了发布登录方法 2 的驱动程序包所需的步骤。

## <a name="obtain-a-software-publisher-certificate-spc"></a>获取软件发布者证书 (SPC)


版本签名需要代码签名证书，也可以简称为软件发行者证书 (SPC) 从商业 CA。

[内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md)主题提供的商业第三方证书颁发机构 (CA) 由 Microsoft 授权列表。 列出的 CA 供应商必须用于提供要释放登录驱动程序包软件发行者证书 (SPC)。

请按照如何获取 SPC 和签名的计算机上安装的专用密钥的 CA 的说明。 请注意 SPC，并请求为其驱动程序程序包进行签名的驱动程序供应商专有检测。 不与请求供应商的组织外部的任何人都必须共享 SPC、 私有密钥和密码。

## <a name="cross-certificates"></a>Cross-Certificates


*从节选*[软件发布者证书](software-publisher-certificate.md):

除了获取一个 SPC，必须获取由 Microsoft 颁发交叉证书。 交叉证书用于验证颁发一个 SPC 的 CA 受信任的根颁发机构。 交叉证书是由另一个 CA 的根证书的公钥进行签名的 CA 颁发的 X.509 证书。 交叉证书允许系统在具有单个受信任的 Microsoft 的根颁发机构，但也提供灵活地扩展到商业 Ca 颁发 SPCs 的信任链。

发布服务器不需要分发与交叉证书[驱动程序包](driver-packages.md)。 交叉证书随数字签名的驱动程序包[编录文件](catalog-files.md)或驱动程序文件中嵌入的签名。 安装驱动程序包的用户无需执行引起的交叉证书的使用任何其他配置步骤。

*所选部分内容摘自*[内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md):

交叉证书是数字证书通过一个证书颁发机构 (CA) 颁发用于签署另一个证书颁发机构的根证书的公钥。 交叉证书提供一种方法创建从单个的受信任的根 CA，到多个其他 Ca 的信任链。

在 Windows 中，交叉证书：

-   允许操作系统内核有单一的受信任的 Microsoft 根颁发机构。
-   将信任链扩展到多个商业 Ca 颁发软件发布者证书 (SPCs)，用于代码签名的软件分发、 安装和在 Windows 上的装载

此处提供了交叉证书用于与 Windows Driver Kit (WDK) 代码签名工具正确签名内核模式软件。 对内核模式软件进行数字签名是类似于代码签名的任何软件的发布的 Windows。 交叉证书为数字签名的开发人员或软件发行者时添加签名的内核模式软件。 交叉证书本身是由代码签名工具添加到的数字签名的二进制文件或目录。

**选择正确的交叉证书**

Microsoft 提供的特定交叉证书用于代码签名的内核模式代码发出 SPCs 每个 CA。 有关交叉证书的详细信息，请参阅[内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md)。 本主题列出了 Microsoft 的名称授权 CA 供应商和正确的交叉证书根颁发机构颁发您 SPC。 查找正确的交叉证书的颁发 CA 供应商的 SPC 和交叉证书下载到您将使用版本签名，并将其存储在驱动程序目录中签名的计算机。 最好在任何签名的命令中使用它时向此证书提供的绝对路径。

## <a name="installing-spc-information-in-the-personal-certificate-store"></a>在个人证书存储中安装 SPC 信息


*更多部分内容摘自*[软件发布者证书](software-publisher-certificate.md):

若要使用一个 SPC 进行签名的驱动程序符合的方式[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)，必须首先中个人信息交换中包含的证书信息 ( *.pfx*)文件。 中包含的信息 *.pfx*然后必须将文件添加到驱动程序进行签名的本地计算机的个人证书存储。

CA 可以颁发 *.pfx*文件，其中包含所需的证书信息。 如果因此，你可以添加。*pfx*中所述的说明的个人证书存储的文件[在个人证书存储中安装.pfx 文件](software-publisher-certificate.md#installing-a-pfx-file-in-the-personal-certificate-store)。

但是，CA 可能会发出对以下文件：

-   一个 *.pvk*文件，其中包含私钥信息。

-   *.Spc*或 *.cer*文件，其中包含公钥信息。

在此情况下，对文件 ( *.pvk*和一个 *.spc，* 或 *.pvk*和一个 *.cer*) 必须转换为 *.pfx*若要将证书信息添加到个人证书存储的文件。

若要创建。*pfx*文件由 CA 颁发的对从文件中，按照这些说明进行操作：

-   要转换 *.pvk*文件和一个 *.spc*文件发送到 *.pfx*文件，请使用以下[ **Pvk2Pfx** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)在命令提示符的命令：

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc myspcfile.spc -pfx mypfxfile.pfx -po pfxpassword -f
    ```

-   要转换 *.pvk*文件和一个 *.cer*文件中，为 *.pfx*文件，请在命令提示符处使用以下 Pvk2Pfx 命令：

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc mycerfile.cer -pfx mypfxfile.pfx -po pfxpassword -f
    ```

以下描述中使用的参数[ **Pvk2Pfx** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)命令：

-   **-Pvk**  *mypvkfile.pvk*参数指定 *.pvk*文件。

-   **-Pi**  *mypvkpassword*选项指定的密码。*pvk*文件。

-   **-Spc** *myspcfile.spc*参数指定 *.spc*文件或 **-spc**  *mycerfile.cer*参数指定 *.cer*文件。

-   **-Pfx** *mypfxfile.pfx*选项指定的名称 *.pfx*文件。

-   **Po** *pfxpassword*选项指定的密码 *.pfx*文件。

-   **-F**选项配置 Pvk2Pfx 替换现有 *.pfx*文件如果存在。

**重要**  应保护 pvk 和 pfx 文件使用强密码。

 

## <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>在个人证书存储中安装一个.pfx 文件


适用于签名的内核模式驱动程序、 证书和密钥存储中的.pfx 文件必须导入到本地的个人证书存储。 Signtool 不支持使用内核模式驱动程序进行签名的.pfx 文件。 限制是由于发生冲突时使用的证书从.pfx 文件的签名中添加交叉证书

*从摘录会最终*[软件发布者证书](software-publisher-certificate.md):

获取后 *.pfx* CA，从文件或创建 *.pfx*从文件 *.pvk*并且。*spc*或 *.cer*文件中，添加中的信息 *.pfx*对进行签名的驱动程序在本地计算机的个人证书存储的文件。 您可以使用证书导入向导导入中的信息 *.pfx*文件到个人证书存储中，按如下所示：

1.  找到 *.pfx*文件位于 Windows 资源管理器，并双击要打开证书导入向导的文件。

2.  按照证书导入向导导入个人证书存储的代码签名证书中的过程。

*从节选*[证书存储区导入一个 SPC](importing-an-spc-into-a-certificate-store.md):

从 Windows Vista 中，一种方法来导入 *.pfx*到本地的个人证书存储的文件是与[CertUtil](https://go.microsoft.com/fwlink/p/?linkid=168888)命令行实用程序。 下面的命令行示例使用 CertUtil 来导入*abc.pfx*的个人证书存储到文件：

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

其中：

-   **-用户**选项指定"当前用户"个人存储区。

-   **-P**选项指定的密码 *.pfx*文件 (*pfxpassword*)。

-   **-ImportPFX**选项指定的名称 *.pfx*文件 (*abc.pfx*)。

## <a name="view-spc-properties"></a>查看 SPC 属性


使用 MMC 证书管理单元 (certmgr.msc) 若要查看的个人证书存储中的证书。

1.  启动 certmgr.msc 管理单元中的证书。
2.  在管理单元的左窗格中，选择个人证书存储文件夹。
3.  单击证书文件夹并双击要用于版本签名的证书。
4.  在证书对话框中的详细信息选项卡上，从要突出显示证书的使用者名称的字段列表中选择使用者。 这是使用 Signtool 的 /n 参数在本部分中的示例中使用的名称。

## <a name="signing"></a>签名


**基于**[版本的驱动程序对程序包进行签名的编录文件](release-signing-a-driver-package-s-catalog-file.md):

运行以下命令以登录的 cat 文件，该驱动程序包进行签名。 /N 命令应使用带引号的证书将在上面，步骤 4 中看到在使用者名称为 CN = MyCompany inc.保留所有权利。

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s My /n “MyCompany Inc.“ /t http://timestamp.verisign.com/scripts/timestamp.dll  toaster.cat
```

/ac 文件名

指定包含要添加到签名块中的其他证书的文件。 这是交叉签名证书，MSCV VSClass3.cer，从 Microsoft 获取交叉证书下载链接。 如果交叉证书不在当前目录中，请使用完整路径名称。 尽管没有要求，则最好对 cat 文件进行签名时添加交叉证书。

/s StoreName

指定要打开时搜索证书存储区。 如果未指定此选项，将打开我的存储，这是个人证书存储区。

/n SubjectName

指定签名证书的使用者的名称。 此值可以是整个主题名称的子字符串。

/t URL

指定的时间戳服务器的 URL。 如果此选项不存在，已签名的文件将不会将时间戳。 **使用时间戳，签署的驱动程序包将一直有效无限期的 SPC 签名证书获取吊销出于其他原因。**

必须遵循每个签名正确另有说明上述步骤，否则你将不能进行签名的驱动程序。 可能会收到如下所示的错误。

```cpp
SignTool Error: No certificates were found that met all the given criteria
```

## <a name="embed-signing"></a>嵌入签名


**基于**[版本签名的驱动程序通过嵌入式签名](release-signing-a-driver-through-an-embedded-signature.md):

从 Windows Vista，内核模式代码签名的策略控制是否将加载的内核模式驱动程序开始。 64 位版本的 Windows 启动 Windows Vista 具有更严格的要求相对于 Windows 的 32 位版本。

内核模式引导启动驱动程序必须具有嵌入的软件发行者证书 (SPC) 签名。 这适用于任何类型的即插即用或为非 PnP 内核模式下启动开始驱动程序。 也适用于 Windows 的 32 位版本。 引导启动驱动程序必须具有嵌入的 SPC 签名、 WHQL 版本签名的编录文件或 SPC 签名的编录文件不是即插即用的内核模式驱动程序。

请参阅[内核模式代码签名要求](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)有关其他信息。

命令为嵌入签名 toaster.sys 文件。

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s my /n “MyCompany Inc. “ /t http://timestamp.verisign.com/scripts/timestamp.dll   toaster.sys
```

签名完成后，运行以下命令来验证签名的驱动程序。

```cpp
signtool verify  /kp  /v  /c  tstamd64.cat  toastpkg.inf
```

命令的输出：

```cpp
Verifying: toaster.inf
File is signed in catalog: toaster.cat
Hash of file (sha1): 580C2A24C3A9E12817E18ADF1C4FE9CF31B01EA3

Signing Certificate Chain:

    Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
    Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
    Expires:   Wed Jul 16 15:59:59 2036
    SHA1 hash: 4EB6D578499B1CCF5F581EAD56BE3D9B6744A5E5

        Issued to: VeriSign Class 3 Code Signing 2010 CA
        Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
        Expires:   Fri Feb 07 15:59:59 2020
        SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F

            Issued to: Contoso, Inc
            Issued by: VeriSign Class 3 Code Signing 2010 CA
            Expires:   Thu Dec 04 15:59:59 2014
            SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269

The signature is timestamped: Mon Jan 27 14:48:55 2014
Timestamp Verified by:
    Issued to: Thawte Timestamping CA
    Issued by: Thawte Timestamping CA
    Expires:   Thu Dec 31 15:59:59 2020
    SHA1 hash: BE36A4562FB2EE05DBB3D32323ADF445084ED656

        Issued to: Symantec Time Stamping Services CA - G2
        Issued by: Thawte Timestamping CA
        Expires:   Wed Dec 30 15:59:59 2020
        SHA1 hash: 6C07453FFDDA08B83707C09B82FB3D15F35336B1

            Issued to: Symantec Time Stamping Services Signer - G4
            Issued by: Symantec Time Stamping Services CA - G2
            Expires:   Tue Dec 29 15:59:59 2020
            SHA1 hash: 65439929B67973EB192D6FF243E6767ADF0834E4
Cross Certificate Chain:
    Issued to: Microsoft Code Verification Root
    Issued by: Microsoft Code Verification Root
    Expires:   Sat Nov 01 05:54:03 2025
    SHA1 hash: 8FBE4D070EF8AB1BCCAF2A9D5CCAE7282A2C66B3     
       
 Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
        Issued by: Microsoft Code Verification Root
        Expires:   Mon Feb 22 11:35:17 2021
        SHA1 hash: 57534CCC33914C41F70E2CBB2103A1DB18817D8B
            
            Issued to: VeriSign Class 3 Code Signing 2010 CA
            Issued by: VeriSign Class 3 Public Primary Certification Authority -  G5
            Expires:   Fri Feb 07 15:59:59 2020
            SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F

                Issued to: Contoso, Inc
                Issued by: VeriSign Class 3 Code Signing 2010 CA
                Expires:   Thu Dec 04 15:59:59 2014
                SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269

Successfully verified: toaster.inf

Number of files successfully Verified: 1
Number of warnings: 0 
Number of errors: 0
```

请注意证书链中的存在 Microsoft 代码验证根。

接下来，检查嵌入 toaster.sys 文件的签名。

```cpp
signtool verify  /v  /kp  toaster.sys
```

命令的输出：

```cpp
Verifying: toaster.sys Hash of file (sha1): CCF5F5C02FEDE87D92FCB7B536DBF5D5EFDB7B41

Signing Certificate Chain:
    Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
    Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
    Expires:   Wed Jul 16 15:59:59 2036
    SHA1 hash: 4EB6D578499B1CCF5F581EAD56BE3D9B6744A5E5

        Issued to: VeriSign Class 3 Code Signing 2010 CA
        Issued by: VeriSign Class 3 Public Primary Certification Authority - G5
        Expires:   Fri Feb 07 15:59:59 2020
        SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F

            Issued to: Contoso, Inc
            Issued by: VeriSign Class 3 Code Signing 2010 CA
            Expires:   Thu Dec 04 15:59:59 2014             SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269 
The signature is timestamped: Mon Jan 27 14:48:55 2014 Timestamp Verified by:
    Issued to: Thawte Timestamping CA     Issued by: Thawte Timestamping CA     Expires:   Thu Dec 31 15:59:59 2020     SHA1 hash: BE36A4562FB2EE05DBB3D32323ADF445084ED656 
        Issued to: Symantec Time Stamping Services CA - G2         Issued by: Thawte Timestamping CA         Expires:   Wed Dec 30 15:59:59 2020         SHA1 hash: 6C07453FFDDA08B83707C09B82FB3D15F35336B1 
            Issued to: Symantec Time Stamping Services Signer - G4             Issued by: Symantec Time Stamping Services CA - G2             Expires:   Tue Dec 29 15:59:59 2020             SHA1 hash: 65439929B67973EB192D6FF243E6767ADF0834E4 
Cross Certificate Chain:
    Issued to: Microsoft Code Verification Root     Issued by: Microsoft Code Verification Root     Expires:   Sat Nov 01 05:54:03 2025     SHA1 hash: 8FBE4D070EF8AB1BCCAF2A9D5CCAE7282A2C66B3         
        Issued to: VeriSign Class 3 Public Primary Certification Authority - G5
        Issued by: Microsoft Code Verification Root
        Expires:   Mon Feb 22 11:35:17 2021
        SHA1 hash: 57534CCC33914C41F70E2CBB2103A1DB18817D8B

            Issued to: VeriSign Class 3 Code Signing 2010 CA
            Issued by: VeriSign Class 3 Public Primary Certification Authority -  G5
            Expires:   Fri Feb 07 15:59:59 2020
            SHA1 hash: 495847A93187CFB8C71F840CB7B41497AD95C64F 
                Issued to: Contoso, Inc                 Issued by: VeriSign Class 3 Code Signing 2010 CA                 Expires:   Thu Dec 04 15:59:59 2014                 SHA1 hash: EFC77FA6BA295580C2A2CD25B56C00606CA21269 
Successfully verified: toaster.sys 
Number of files successfully Verified: 1 Number of warnings: 0 Number of errors: 0 
```

同样，请注意证书链中的存在 Microsoft 代码验证根。

 

 





