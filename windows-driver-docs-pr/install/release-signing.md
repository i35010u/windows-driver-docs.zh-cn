---
title: 发布签名
description: 完成测试签名并验证驱动程序是否已准备好进行发布后, 必须对驱动程序包进行签名。 可以通过两种方式对驱动程序包进行签名。
ms.assetid: 71499A0A-95D0-411C-84D1-C4B91FA4E6B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6d18ca5172ccb1159c9615229f5a675b0506dd
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063933"
---
# <a name="release-signing"></a>发布签名


完成测试签名并验证驱动程序是否已准备好进行发布后, 必须对驱动程序包进行签名。 可以通过两种方式对驱动程序包进行签名。

版本签名标识加载到 Windows Vista 和更高版本的 Windows 中的内核模式或用户模式二进制文件 (如 .sys 或 .dll 文件) 的发布者。

内核模式二进制文件通过以下任一方法进行释放:

1.  Windows 硬件质量实验室 (WHQL 也称为 Winqual) 发布对驱动程序包的签名。 WHQL 版本签名通过 Windows 认证计划获取。 下面的链接描述了从 Windows 认证计划开始到完成的五个步骤。 有关此选项的更多详细信息, 请参阅[Windows 硬件认证: 从此处开始](https://docs.microsoft.com/previous-versions/hh833792(v=msdn.10))。 以上链接中的步骤的任何问题都应该定向到<sysdev@microsft.com>别名。
2.  驱动程序开发人员和供应商可以对驱动程序包进行签名, 而不是使用 WHQL 程序。 此程序已从 Vista OS 版本开始。 版本签名是通过软件发行者证书 (SPC) 创建的。 SPC 是从 Microsoft 授权的第三方证书颁发机构 (CA) 获取的, 用于颁发此类证书。 此类 SPC 生成的签名还符合 Windows Vista 和更高版本的 windows Vista 和32位版本的 PnP 驱动程序签名64要求

接下来介绍为方法2发布签名驱动程序包所需的步骤。

## <a name="obtain-a-software-publisher-certificate-spc"></a>获取软件发行者证书 (SPC)


版本签名需要一个代码签名证书, 也称为商业 CA 颁发的软件发行者证书 (SPC)。

[内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md)主题提供了 Microsoft 授权的商业第三方证书颁发机构 (CA) 的列表。 列出的 CA 供应商必须用来提供软件发行者证书 (SPC) 才能对驱动程序包进行签名。

按照 CA 有关如何获取 SPC 并在签名计算机上安装私钥的说明进行操作。 请注意, SPC 是要求它对其驱动程序包进行签名的驱动程序供应商的专有检测。 SPC、私钥和密码不得与请求供应商的组织外部的任何人共享。

## <a name="cross-certificates"></a>交叉证书


*摘录自*[软件发行者证书](software-publisher-certificate.md):

除了获取 SPC 外, 还必须获取 Microsoft 颁发的交叉证书。 使用交叉证书来验证颁发 SPC 的 CA 是否为受信任的根证书颁发机构。 交叉证书是由 CA 颁发的 x.509 证书, 用于对另一 CA 的根证书的公钥进行签名。 跨证书允许系统拥有单个受信任的 Microsoft 根证书颁发机构, 还可以灵活地将信任链扩展到颁发 SPCs 的商业 Ca。

发布者不必使用[驱动程序包](driver-packages.md)分发交叉证书。 交叉证书包含在驱动程序包的[目录文件](catalog-files.md)的数字签名或嵌入到驱动程序文件中的签名。 安装驱动程序包的用户无需执行任何其他配置步骤, 因为使用了交叉证书。

*选择的摘录*[内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md):

交叉证书是由一个证书颁发机构 (CA) 颁发的数字证书, 用于对其他证书颁发机构的根证书的公钥进行签名。 跨证书提供了一种方法, 用于创建从一个受信任的根 CA 到多个其他 Ca 的信任链。

在 Windows 中, 交叉证书:

-   允许操作系统内核具有单个受信任的 Microsoft 根证书颁发机构。
-   向颁发软件发行者证书 (SPCs) 的多个商业 Ca 扩展信任链, 该证书用于在 Windows 上进行分发、安装和加载的代码签名软件

此处提供的交叉证书适用于 Windows 驱动程序工具包 (WDK) 代码签名工具, 用于对内核模式软件进行正确的签名。 对内核模式软件进行数字签名类似于对 Windows 发布的任何软件进行代码签名。 在对内核模式软件进行签名时, 开发人员或软件发行者会将交叉证书添加到数字签名。 代码签名工具将跨证书本身添加到二进制文件或目录的数字签名。

**选择正确的交叉证书**

Microsoft 为每个 CA 提供了一个特定的交叉证书, 用于为代码签名内核模式代码颁发 SPCs。 有关交叉证书的详细信息, 请参阅[用于内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md)。 本主题列出了 Microsoft 授权的 CA 供应商的名称, 以及颁发 SPC 的根颁发机构的正确交叉证书。 找到 CA 供应商颁发的 SPC 的正确交叉证书, 并将交叉证书下载到要用于发布签名的签名计算机, 然后将其存储在驱动程序目录中。 建议在任何签名命令中使用此证书时提供该证书的绝对路径。

## <a name="installing-spc-information-in-the-personal-certificate-store"></a>在个人证书存储中安装 SPC 信息


*进一步摘录*[软件发行者证书](software-publisher-certificate.md):

为了使用 SPC 对驱动程序进行签名的方式符合[内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md), 必须首先将证书信息包含在个人信息交换 ( *.pfx*) 文件中。 然后, 必须将 *.pfx*文件中包含的信息添加到对驱动程序进行签名的本地计算机的 "个人" 证书存储中。

CA 可能会颁发包含所需证书信息的 *.pfx*文件。 如果是这样, 您可以添加。*pfx*文件保存到个人证书存储中, 请按照在[个人证书存储中安装 .pfx 文件](software-publisher-certificate.md#installing-a-pfx-file-in-the-personal-certificate-store)中所述的说明进行操作。

但是, CA 可能会发出下列文件对:

-   一个包含私钥信息的*pvk*文件。

-   包含公钥信息的 *.spc*或 *.cer*文件。

在这种情况下, 必须将一对文件 ( *pvk*和 *.spc,* 或*pvk*和 *.cer*) 转换为 *.Pfx*文件, 才能将证书信息添加到个人证书存储区。

来创建。*pfx*文件, 请按照以下说明进行操作:

-   若要将*pvk*文件和 *.spc*文件转换为 *.pfx*文件, 请在命令提示符处使用以下[**Pvk2Pfx**](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)命令:

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc myspcfile.spc -pfx mypfxfile.pfx -po pfxpassword -f
    ```

-   若要将*pvk*文件和 *.cer*文件转换为 *.pfx*文件, 请在命令提示符处使用以下 Pvk2Pfx 命令:

    ```cpp
    Pvk2Pfx -pvk mypvkfile.pvk -pi mypvkpassword -spc mycerfile.cer -pfx mypfxfile.pfx -po pfxpassword -f
    ```

下面介绍了[**Pvk2Pfx**](https://docs.microsoft.com/windows-hardware/drivers/devtest/pvk2pfx)命令中使用的参数:

-   **-Pvk**  *mypvkfile. pvk*参数指定*pvk*文件。

-   **-Pi**  *mypvkpassword*选项指定的密码。*pvk*文件。

-   **-Spc** *myspcfile*参数指定一个 *.spc*文件或 **-spc**  *mycerfile*参数指定 *.cer*文件。

-   **-Pfx** *mypfxfile*选项指定 *.pfx*文件的名称。

-   **-Po** *pfxpassword*选项指定 *.pfx*文件的密码。

-   **-F**选项将 Pvk2Pfx 配置为替换现有*的 .pfx*文件 (如果存在)。

**重要说明**  应该用强密码保护 pvk 和 pfx 文件。

 

## <a name="installing-a-pfx-file-in-the-personal-certificate-store"></a>在个人证书存储中安装 .pfx 文件


若要为内核模式驱动程序签名, 则必须将存储在 .pfx 文件中的证书和密钥导入到本地个人证书存储中。 Signtool 不支持使用 .pfx 文件对内核模式驱动程序进行签名。 限制是由于在使用 .pfx 文件中的证书时在签名中添加交叉证书发生冲突

*最终摘录*[软件发行者证书](software-publisher-certificate.md):

从 CA 获取 *.pfx*文件或从*pvk*创建 *.pfx*文件后, 也可以从。*spc*或 *.cer*文件, 请将 *.pfx*文件中的信息添加到对驱动程序进行签名的本地计算机的 "个人" 证书存储中。 您可以使用证书导入向导将 *.pfx*文件中的信息导入到个人证书存储, 如下所示:

1.  在 Windows 资源管理器中找到 *.pfx*文件, 然后双击该文件以打开证书导入向导。

2.  按照证书导入向导中的步骤将代码签名证书导入到个人证书存储区中。

*摘录自*将[SPC 导入到证书存储中](importing-an-spc-into-a-certificate-store.md):

从 Windows Vista 开始, 将 *.pfx*文件导入到本地个人证书存储中的另一种方法是使用[CertUtil](https://go.microsoft.com/fwlink/p/?linkid=168888)命令行实用程序。 以下命令行示例使用 CertUtil 将*abc*文件导入到个人证书存储中:

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

其中：

-   **-User**选项指定 "当前用户" 的个人存储。

-   **-P**选项指定 *.pfx*文件的密码 (*pfxpassword*)。

-   **-ImportPFX**选项指定 *.pfx*文件的名称 (*abc*)。

## <a name="view-spc-properties"></a>查看 SPC 属性


使用 MMC "证书" 管理单元 (certmgr.msc) 查看个人证书存储中的证书。

1.  启动 "证书" 管理单元 certmgr.msc。
2.  在管理单元的左窗格中, 选择 "个人证书存储区" 文件夹。
3.  单击 "证书" 文件夹, 然后双击要用于 "发布签名" 的证书。
4.  在 "证书" 对话框的 "详细信息" 选项卡上, 从字段列表中选择 "使用者", 突出显示证书的使用者名称。 这是本部分的示例中用于 Signtool 的/n 参数的名称。

## <a name="signing"></a>签名


**基于**[对驱动程序包的目录文件进行发布签名](release-signing-a-driver-package-s-catalog-file.md):

运行以下命令对对驱动程序包进行签名的 cat 文件进行签名。 /N 命令应使用前面步骤4中的 "使用者" 中所示的带引号的证书名称作为 CN = MyCompany Inc.。

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s My /n “MyCompany Inc.“ /t http://timestamp.digicert.com toaster.cat
```

/ac FileName

指定包含要添加到签名块的附加证书的文件。 这是从 Microsoft 交叉证书下载链接获取的交叉签名证书 MSCV-VSClass3。 如果交叉证书不在当前目录中, 请使用完整路径名称。 尽管不是必需的, 但建议在对 cat 文件进行签名时添加交叉证书。

/s StoreName

指定要在搜索证书时打开的存储区。 如果未指定此选项, 则打开 "我的存储", 这是个人证书存储区。

/n SubjectName

指定签名证书的主题的名称。 此值可以是整个主题名称的子字符串。

/t URL

指定时间戳服务器的 URL。 如果此选项不存在, 则不会对签名的文件进行时间戳。 **对于时间戳, 签署的驱动程序包会无限期地保持有效, 直到出于其他原因吊销 SPC 签名证书。**

必须按照上述说明正确执行每个签名步骤, 否则将无法对驱动程序进行签名。 可能会出现如下错误。

```cpp
SignTool Error: No certificates were found that met all the given criteria
```

## <a name="embed-signing"></a>嵌入签名


**基于**[通过嵌入签名对驱动程序进行发布签名](release-signing-a-driver-through-an-embedded-signature.md):

从 Windows Vista 开始, 内核模式代码签名策略控制是否将加载内核模式驱动程序。 64位版本的 Windows (从 Windows Vista 开始) 与32位版本的 Windows 相比要求更严格。

内核模式启动启动驱动程序必须具有嵌入式软件发行者证书 (SPC) 签名。 这适用于任何类型的 PnP 或非 PnP 内核模式启动驱动程序。 还适用于32位版本的 Windows。 不是启动启动驱动程序的 PnP 内核模式驱动程序必须具有嵌入的 SPC 签名、具有 WHQL 版本签名的目录文件或具有 SPC 签名的目录文件。

有关其他信息, 请参阅[内核模式代码签名要求](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)。

用于嵌入 toaster 文件的命令。

```cpp
signtool sign /v /ac MSCV-VSClass3.cer /s my /n “MyCompany Inc. “ /t http://timestamp.digicert.com toaster.sys
```

完成签名后, 运行以下命令以验证签名的驱动程序。

```cpp
signtool verify  /kp  /v  /c  tstamd64.cat  toastpkg.inf
```

命令输出:

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

请注意, 证书链中存在 Microsoft 代码验证根。

接下来, 请检查 toaster 文件的嵌入签名。

```cpp
signtool verify  /v  /kp  toaster.sys
```

命令输出:

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

同样, 请注意证书链中是否存在 Microsoft 代码验证根。

 

 





