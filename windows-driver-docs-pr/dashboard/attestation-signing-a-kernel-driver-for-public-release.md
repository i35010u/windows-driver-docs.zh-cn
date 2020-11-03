---
title: 对内核驱动程序进行证明签名以便公开发布
description: 本主题介绍如何使用证明签名对驱动程序签名。
ms.assetid: A292B15D-37FD-407E-998C-728D9423E712
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b9d8a6f223788128c8239c0d46cf4e725af4eed
ms.sourcegitcommit: 6c736c8a461f82f41f9c6988a20de2a2098ab482
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "92914024"
---
# <a name="attestation-signing-a-kernel-driver-for-public-release"></a>对内核驱动程序进行证明签名以便公开发布

本主题介绍如何使用证明签名对驱动程序签名。

> [!Note]
> 证明签名具有下列属性。
>
> - 证明签名支持 Windows 10 桌面版内核模式和用户模式驱动程序。 尽管用户模式驱动程序无需由适用于 Windows 10 的 Microsoft 进行签名，但相同的证明过程可以同时用于用户和内核模式驱动程序。
> - 证明签名不会返回 **ELAM** 的正确 PE 级别或 **Windows Hello** PE 二进制文件。  它们必须经过测试，并且以 .hlkx 包的形式提交，以便接收额外的签名属性。
> - 证明签名需要使用 EV 证书，才能将驱动程序提交到合作伙伴中心（硬件开发人员中心仪表板）。
> - 已进行证明签名的驱动程序适用于 Windows 10。 它不适用于早期版本的 Windows（例如 Windows 8.1 和 Windows 7），并且不受 Windows Server 2016 及更高版本支持。
> - 证明签名要求驱动程序文件夹名称不包含特殊字符、不包含 UNC 文件共享路径，并且长度小于 40 个字符。
> - 当驱动程序收到证明签名时，不会进行 Windows 认证。 Microsoft 证明签名表明驱动程序受 Windows 信任，但由于该驱动程序未在 HLK Studio 中进行测试，因此不能保证兼容性、功能等。
> - 要使你的驱动程序得到 Windows 认证，请将 HLK Studio 生成的 .hlkx 包提交到合作伙伴中心。
> - 要对驱动程序证明进行签名，请提交 CAB 文件。

## <a name="attestation-signing-a-kernel-mode-driver"></a>对内核模式驱动程序进行证明签名

若要对内核模式驱动程序进行证明签名，请完成以下步骤：

1. 获取 EV 代码签名证书（进行步骤 2 的要求。）
2. 向合作伙伴中心注册你的公司
3. 下载并安装 Windows 驱动程序工具包
4. 创建 CAB 文件提交
5. 使用 EV 证书对 CAB 文件提交签名
6. 使用合作伙伴中心提交 EV 签名的 Cab 文件
7. 验证驱动程序是否已正确签名
8. 在 Windows 10 桌面版上测试驱动程序

## <a name="acquire-an-ev-code-signing-certificate"></a>获取 EV 代码签名证书

在向仪表板提交要签名的二进制文件前，需要获取扩展验证 (EV) 代码签名证书，才能确保数字信息安全。 EV 证书是建立所提交的代码所有权的公认标准。

按照[获取代码签名证书](get-a-code-signing-certificate.md)中的步骤设置 EV 证书。

## <a name="allowable-pe-signatures-and-binaries"></a>允许的 PE 签名和二进制文件

下列 PE 级别和二进制文件可通过证明处理：

- **PeTrust**
- **DrmLevel**
- **HAL**
- .exe
- .cab
- .dll
- .ocx
- .msi
- .xpi
- .xap

## <a name="register-your-company-for-partner-center-services"></a>向合作伙伴中心服务注册你的公司

若要通过合作伙伴中心对驱动程序进行签名，首先需要注册你的组织并获得代码签名证书。

请按照[注册硬件计划](register-for-the-hardware-program.md)中所述过程设置将用于硬件仪表板的帐户。

## <a name="download-and-install-the-windows-driver-kit"></a>下载并安装 Windows 驱动程序工具包

你需要下载并安装 Windows 驱动程序工具包 (WDK)，才能访问用于签署驱动程序二进制文件的工具。

按照[下载适用于 Windows 10 的工具包和工具](/windows-hardware/get-started/adk-install)中描述的过程下载并安装 WDK。

## <a name="create-a-cab-files-submission"></a>创建 CAB 文件提交

若要创建可提交至仪表板的 CAB 文件，请完成以下步骤：

1. 收集将在单个目录中提交以进行签名的二进制文件。 在此示例中，我们将使用 C:\\Echo。 此处所述的步骤将引用 GitHub 中提供的[回显驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf/driver/AutoSync)。

典型的 CAB 文件提交包含以下内容：

- 驱动程序本身，例如 Echo.sys
- 仪表板用来促进签名过程的驱动程序 INF 文件。
- 符号文件，用于调试信息。 例如，Echo.pdb。
- 目录 .CAT 文件是必需的，仅用于公司验证。 Microsoft 会重新生成目录文件，并替换已提交的任何目录文件。

  > [!NOTE]
  > CAB 文件中的每个驱动程序文件夹都必须支持同一组体系结构。 例如，它们必须支持 x86、x64，或者全都必须同时支持 x86 和 x64。
  >
  > 引用驱动程序位置 (\\\server\share) 时，请勿使用 UNC 文件共享路径。  必须使用映射的驱动器号才能使 CAB 有效。

2. 使用 MakeCab.exe 处理 DDF 文件并创建 cab 文件。

以管理员身份打开命令提示符窗口。 然后输入以下命令以查看 MakeCab 选项：

MakeCab /?

```cpp
C:\Echo> MakeCab /?
Cabinet Maker - Lossless Data Compression Tool

MAKECAB [/V[n]] [/D var=value ...] [/L dir] source [destination]
MAKECAB [/V[n]] [/D var=value ...] /F directive_file [...]

  source         File to compress.
  destination    File name to give compressed file.  If omitted, the
                 last character of the source file name is replaced
                 with an underscore (_) and used as the destination.
  /F directives  A file with MakeCAB directives (may be repeated). Refer to
                 Microsoft Cabinet SDK for information on directive_file.
  /D var=value   Defines variable with specified value.
  /L dir         Location to place destination (default is current directory).
  /V[n]          Verbosity level (1..3).
```

3. 准备 cab 文件 DDF 输入文件。 对于我们的回显驱动程序，它可能看起来如下所示。

```cpp
;**_ Echo.ddf example
;
.OPTION EXPLICIT     ; Generate errors
.Set CabinetFileCountThreshold=0
.Set FolderFileCountThreshold=0
.Set FolderSizeThreshold=0
.Set MaxCabinetSize=0
.Set MaxDiskFileCount=0
.Set MaxDiskSize=0
.Set CompressionType=MSZIP
.Set Cabinet=on
.Set Compress=on
;Specify file name for new cab file
.Set CabinetNameTemplate=Echo.cab
; Specify the subdirectory for the files.  
; Your cab file should not have files at the root level,
; and each driver package must be in a separate subfolder.
.Set DestinationDir=Echo
;Specify files to be included in cab file
C:\Echo\Echo.Inf
C:\Echo\Echo.Sys
```

4. 调用 makecab 实用工具，并使用 /f 选项将 ddf 文件作为输入提供。

```cpp
C:\Echo> MakeCab /f "C:\Echo\Echo.ddf
```

makecab 的输出应该显示示例 2 中创建的 Cabinet 中的文件数。

```cpp
C:\Echo> MakeCab /f Echo.ddf
Cabinet Maker - Lossless Data Compression Tool

17,682 bytes in 2 files
Total files:              2
Bytes before:        17,682
Bytes after:          7,374
After/Before:            41.70% compression
Time:                     0.20 seconds ( 0 hr  0 min  0.20 sec)
Throughput:              86.77 Kb/second
```

5. 在 Disk1 子目录中找到 cab 文件。 可以在文件资源管理器中选择 cab 文件，以验证它是否包含预期的文件。

## <a name="sign-the-submission-cab-file-with-your-ev-certificate"></a>使用 EV 证书对提交 CAB 文件签名

1. 使用 EV 证书提供商推荐的过程通过 EV 证书对 cab 文件进行签名。例如，使用 SHA256 证书/摘要算法/时间戳对 .CAB 进行签名  

```cpp
C:\Echo> SignTool sign /ac "C:\MyEVCert.cer" /s MY /n "Company Name" /fd sha256 /tr http://sha256timestamp.ws.symantec.com/sha256/timestamp /td sha256 /v "C:\Echo\Disk1\Echo.cab"
```

> [!IMPORTANT]
> 切记使用行业最佳做法管理 EV 代码签名过程的安全性。

## <a name="submit-the-ev-signed-cab-file-using-the-partner-center"></a>使用合作伙伴中心提交 EV 签名的 Cab 文件

1. 使用合作伙伴中心提交 EV 签名的 CAB 文件。 有关详细信息，请参阅[驱动程序签名属性](../develop/driver-signing-properties.md)。

   - 在完成证明提交的过程中，请勿勾选在下面突出显示的任何测试签名框。  让它们保持取消选中状态。

   - 以下屏幕截图显示了用于提交回显驱动程序进行签名的选项。
    ![显示用于提交回显驱动程序进行签名的选项的屏幕截图](images/Attestation-Flow.PNG)

2. 签名过程完成后，请从硬件仪表板下载已签名的驱动程序。

## <a name="validate-that-the-driver-was-properly-signed"></a>验证驱动程序是否已正确签名

完成以下步骤以确保驱动程序已正确签名。

1. 下载提交文件后，提取驱动程序文件。

2. 以管理员身份打开命令提示符窗口。 然后，输入以下命令来验证驱动程序是否已按预期签名。

```cpp
C:\Echo> SignTool verify Echo.Sys
```

3. 若要列出附加信息，并使 signtool 验证包含多个签名的文件中的所有签名，请键入以下命令。

```cpp
C:\Echo> SignTool verify /pa /ph /v /d Echo.Sys
```

4. 若要确认驱动程序的 EKU，请完成以下步骤。
a. 打开 Windows 资源管理器并找到二进制文件。 选择并按住（或右键单击）该文件并选择“属性”。
b. 在“数字签名”  选项卡上，选择“签名列表”中列出的项。
c. 选择“详细信息”  按钮，然后选择“查看证书”  。
d. 在“详细信息”  选项卡上，选择“增强型密钥用法”  字段。
当驱动程序由仪表板重新签名时，使用以下过程。

- 附加 Microsoft SHA2 嵌入式签名。
- 如果客户使用自己的证书对驱动程序二进制文件进行嵌入式签名，将不会覆盖这些签名。
- 创建新的目录文件并使用 SHA2 Microsoft 证书对该目录文件签名。 该目录会替换客户提供的任何现有目录。

## <a name="test-your-driver-on-windows-10"></a>在 Windows 10 上测试驱动程序

使用以下说明安装示例驱动程序。

1. 打开设备管理器、选择并按住（或右键单击）计算机图标，然后选择“添加过时硬件”。 按照提示完成驱动程序的安装。

2. 或者，以管理员身份打开“命令提示符”窗口并使用 devcon 安装驱动程序。 导航到你的驱动程序包文件夹，然后输入以下命令。

```cpp
C:\Echo> devcon install echo.inf root\ECHO
```

3. 确认驱动程序安装过程不会显示“Windows 无法验证该驱动程序软件的发布者。” “Windows 安全”对话框。

## <a name="create-a-submission-with-multiple-drivers"></a>创建包含多个驱动程序的提交

若要同时提交多个驱动程序，请为每个驱动程序创建一个子目录，如下所示。

![显示示例驱动程序签名目录结构的图像。](images/multiple-driversigning.png)

准备一个引用子目录的 CAB 文件 DDF 输入文件。 它可能如下所示：

```cpp
;*** Submission.ddf multiple driver example
;
.OPTION EXPLICIT     ; Generate errors
.Set CabinetFileCountThreshold=0
.Set FolderFileCountThreshold=0
.Set FolderSizeThreshold=0
.Set MaxCabinetSize=0
.Set MaxDiskFileCount=0
.Set MaxDiskSize=0
.Set CompressionType=MSZIP
.Set Cabinet=on
.Set Compress=on
;Specify file name for new cab file
.Set CabinetNameTemplate=Echo.cab
;Specify files to be included in cab file
; First Driver
.Set DestinationDir=DriverPackage1
C:\DriverFiles\DriverPackage1\Driver1.sys
C:\DriverFiles\DriverPackage1\Driver1.inf
; Second driver
.Set DestinationDir=DriverPackage2
C:\DriverFiles\DriverPackage2\Driver2.sys
C:\DriverFiles\DriverPackage2\Driver2.inf
```

可以按照以下步骤对要提交的其他驱动程序文件进行签名、提交和测试。
