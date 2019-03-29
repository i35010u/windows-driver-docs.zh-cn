---
title: 对内核驱动程序进行证明签名以便公开发布
author: DOMARS
redirect_url: https://msdn.microsoft.com/library/windows/hardware/mt786448
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4cd26934d8e9a77cec307504b66f986b460794
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464315"
---
# <a name="attestation-signing-a-kernel-driver-for-public-release"></a>对内核驱动程序进行证明签名以便公开发布

本主题介绍如何通过 Windows 硬件开发人员中心仪表板 Web 门户使用证明签名签署驱动程序。

**注意** 证明签名具有下列属性。

 - 证明签名支持 Windows 10 桌面版内核模式和用户模式驱动程序。 尽管用户模式驱动程序无需由适用于 Windows 10 的 Microsoft 进行签名，但相同的证明过程可以同时用于用户和内核模式驱动程序。
 - 证明签名需要使用 EV 证书，才能将驱动程序提交到硬件开发人员中心仪表板。
 - 证明签名的驱动程序仅适用于 Windows 10 桌面版；它不适用于其他版本的 Windows，例如 Windows Server 2016、Windows 8.1 或 Windows 7。




## <a name="span-idattestationsigningakernelmodedriverspanspan-idattestationsigningakernelmodedriverspanspan-idattestationsigningakernelmodedriverspanattestation-signing-a-kernel-mode-driver"></a><span id="Attestation_Signing_a_Kernel_Mode_Driver"></span><span id="attestation_signing_a_kernel_mode_driver"></span><span id="ATTESTATION_SIGNING_A_KERNEL_MODE_DRIVER"></span>对内核模式驱动程序进行证明签名


若要对内核模式驱动程序进行证明签名，请完成以下步骤：

1. 获取 EV 代码签名证书
2. 为 Windows 硬件仪表板服务注册你的公司
3. 下载并安装 Windows 驱动程序工具包
4. 创建 CAB 文件提交
5. 使用 EV 证书对 CAB 文件提交签名
6. 使用硬件开发人员中心仪表板提交 EV 签名的 Cab 文件
7. 验证驱动程序是否已正确签名
8. 在 Windows 10 桌面版上测试驱动程序<span id="Acquire_an__EV_Code_Signing_Certificate"></span><span id="acquire_an__ev_code_signing_certificate"></span><span id="ACQUIRE_AN__EV_CODE_SIGNING_CERTIFICATE"></span>获取 EV 代码签名证书


在可以使用要进行签名的仪表板提交二进制文件前，需要获取扩展验证 (EV) 代码签名证书，才能确保数字信息安全。 此证书是用于建立你的公司对你所提交代码的所有权的接受标准。 它让你可以用数字形式签署 PE 二进制文件，例如 .exe、.cab、.dll、.ocx、.msi、.xpi 和 .xap 文件。

按照[获取代码签名证书](https://msdn.microsoft.com/library/windows/hardware/hh801887.aspx)中描述的过程获取所需的 EV 代码签名证书。

## <a name="span-idregisteryourcompanyforwindowshardwaredashboardservicesspanspan-idregisteryourcompanyforwindowshardwaredashboardservicesspanspan-idregisteryourcompanyforwindowshardwaredashboardservicesspanregister-your-company-for-windows-hardware-dashboard-services"></a><span id="Register_your_company_for_Windows_Hardware_Dashboard_Services"></span><span id="register_your_company_for_windows_hardware_dashboard_services"></span><span id="REGISTER_YOUR_COMPANY_FOR_WINDOWS_HARDWARE_DASHBOARD_SERVICES"></span>为 Windows 硬件仪表板服务注册你的公司


可以使用硬件开发人员中心仪表板对你的设备和应用进行硬件认证。 若要访问硬件开发人员中心仪表板，需要注册自己的公司并获取代码签名证书。

按照[登录之前](https://msdn.microsoft.com/library/windows/hardware/br230782)中描述的过程设置仪表板上所需的帐户。

## <a name="span-iddownloadandinstallthewindowsdriverkitspanspan-iddownloadandinstallthewindowsdriverkitspanspan-iddownloadandinstallthewindowsdriverkitspan-download-and-install-the-windows-driver-kit"></a><span id="_Download_and_install_the_Windows_Driver_Kit"></span><span id="_download_and_install_the_windows_driver_kit"></span><span id="_DOWNLOAD_AND_INSTALL_THE_WINDOWS_DRIVER_KIT"></span>下载并安装 Windows 驱动程序工具包


你将需要下载并安装 Windows 驱动程序工具包 (WDK)，才能获得对用于签署二进制文件的工具的访问权限。

按照[下载适用于 Windows 10 的工具包和工具](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)中描述的过程下载并安装 WDK。

## <a name="span-idcreateacabfilessubmissionspanspan-idcreateacabfilessubmissionspanspan-idcreateacabfilessubmissionspancreate-a-cab-files-submission"></a><span id="Create_a_CAB_Files_Submission"></span><span id="create_a_cab_files_submission"></span><span id="CREATE_A_CAB_FILES_SUBMISSION"></span>创建 CAB 文件提交


若要创建适用于仪表板的 CAB 文件提交，请完成以下步骤。

1. 收集将在单个目录中提交以进行签名的二进制文件。 在此示例中，我们将使用 C:\\Echo。 此处所述的步骤将在该位置引用 GitHub 中提供的回显驱动程序。

[https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf/driver/AutoSync](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo/kmdf/driver/AutoSync)

  典型的 cab 文件提交包含以下内容。

  -   驱动程序本身，例如 Echo.sys
  -   仪表板用来促进签名过程的驱动程序 INF 文件。
  -   不需要目录 .CAT 文件。 Microsoft 会重新生成目录文件，并替换已提交的任何目录文件。 Microsoft 提供的替换目录也进行了签名。

2. 使用 MakeCab.exe 处理 DDF 文件并创建 cab 文件。

   以管理员身份打开命令提示符窗口。 然后输入以下命令以查看 MakeCab 选项：

   MakeCab /?

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; MakeCab /?
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
    /V[n]          Verbosity level (1..3).</code></pre></td>
   </tr>
   </tbody>
   </table>

3. 准备 cab 文件 DDF 输入文件。 对于我们的回显驱动程序，它可能看起来如下所示。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>; *** Echo.ddf example ***
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
   ; Specify file name for new cab file
   .Set CabinetNameTemplate=Echo.cab
   ; Specify the subdirectory for the files.  
   ; Your cab file should not have files at the root level, 
   ; and each driver package must be in a separate subfolder.
   .Set DestinationDir=Echo
   ; Specify files to be included in cab file
   C:\Echo\Echo.Inf
   C:\Echo\Echo.Sys</code></pre></td>
   </tr>
   </tbody>
   </table>

   **注意**CAB 中的所有驱动程序文件夹必须支持同一组体系结构，例如，所有驱动程序必须为 x86、所有驱动程序必须为 x64 或所有驱动程序必须同时支持 x86 和 x64。

4. 调用 makecab 实用工具，并使用 /f 选项将 ddf 文件作为输入提供。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; MakeCab /f "C:\Echo\Echo.ddf</code></pre></td>
   </tr>
   </tbody>
   </table>

   makecab 的输出应该显示示例 2 中创建的 Cabinet 中的文件数。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; MakeCab /f Echo.ddf
   Cabinet Maker - Lossless Data Compression Tool

   17,682 bytes in 2 files
   Total files:              2
   Bytes before:        17,682
   Bytes after:          7,374
   After/Before:            41.70% compression
   Time:                     0.20 seconds ( 0 hr  0 min  0.20 sec)
   Throughput:              86.77 Kb/second</code></pre></td>
   </tr>
   </tbody>
   </table>

5. 在 Disk1 子目录中找到 cab 文件。 可以在文件资源管理器中单击 cab 文件，以验证它是否包含预期的文件。

## <a name="span-idsignthesubmissioncabfilewithyourevcertspanspan-idsignthesubmissioncabfilewithyourevcertspanspan-idsignthesubmissioncabfilewithyourevcertspansign-the-submission-cab-file-with-your-ev-cert"></a><span id="Sign_the_Submission_Cab_File__with_your_EV_Cert"></span><span id="sign_the_submission_cab_file__with_your_ev_cert"></span><span id="SIGN_THE_SUBMISSION_CAB_FILE__WITH_YOUR_EV_CERT"></span>使用 EV 证书对提交 Cab 文件签名


1. 使用 EV 证书提供商推荐的过程通过 EV 证书对 cab 文件进行签名。例如，可以使用 signtool，如果使用的是 Verisign，则可以指定其时间戳服务器。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; SignTool sign /v /s MY /n "Subject Name of the Signing Certificate" /t http://timestamp.verisign.com/scripts/timstamp.dll "C:\Echo\Disk1\Echo.cab"</code></pre></td>
   </tr>
   </tbody>
   </table>

   **注意**  使用行业最佳做法管理 EV 证书签名过程的安全性。



## <a name="span-idsubmittheevsignedcabfileusingthewindowshardwaredevelopercenterdashboardspanspan-idsubmittheevsignedcabfileusingthewindowshardwaredevelopercenterdashboardspanspan-idsubmittheevsignedcabfileusingthewindowshardwaredevelopercenterdashboardspansubmit-the-ev-signed-cab-file-using-the-hardware-dev-center-dashboard"></a><span id="Submit_the_EV_signed_Cab_file_using_the__Windows_Hardware_Developer_Center_Dashboard"></span><span id="submit_the_ev_signed_cab_file_using_the__windows_hardware_developer_center_dashboard"></span><span id="SUBMIT_THE_EV_SIGNED_CAB_FILE_USING_THE__WINDOWS_HARDWARE_DEVELOPER_CENTER_DASHBOARD"></span>使用硬件开发人员中心仪表板提交 EV 签名的 Cab 文件


1. 使用硬件开发人员中心仪表板提交 EV 签名的 Cab 文件。 有关详细信息，请参阅[驱动程序签名属性](driver-signing-properties.md)和[文件签名服务](https://msdn.microsoft.com/Library/Windows/Hardware/Dn771767.aspx)。

作为提交过程的一部分，你将指出提交中的所有驱动程序支持哪些体系结构。 使用复选框提供了三个选项。

-   x86
-   x64
-   x86 和 x64

CAB 中的所有驱动程序文件夹必须支持同一组体系结构，例如，所有驱动程序必须为 x86、所有驱动程序必须为 x64 或同时支持 x86 和 x64。 如果具有支持不同体系结构组合的驱动程序，请创建单独的提交。

还需要表明是否要提交通用驱动程序。 有关详细信息，请参阅[通用 Windows 驱动程序入门](getting-started-with-universal-drivers.md)。

以下屏幕截图显示了用于提交回显驱动程序进行签名的选项。

![驱动程序签名提交选项](images/attestation-driver-signing-submission-dashboard.png)

2. 签名过程完成后，请从硬件开发人员中心仪表板下载已签名的驱动程序。
   ## <a name="span-idvalidatethatthedriverwasproperlysignedspanspan-idvalidatethatthedriverwasproperlysignedspanspan-idvalidatethatthedriverwasproperlysignedspanvalidate-that-the-driver-was-properly-signed"></a><span id="Validate_that_the_driver_was_properly_signed"></span><span id="validate_that_the_driver_was_properly_signed"></span><span id="VALIDATE_THAT_THE_DRIVER_WAS_PROPERLY_SIGNED"></span>验证驱动程序是否已正确签名


完成以下步骤以验证驱动程序是否已正确签名

1. 下载提交文件后，提取驱动程序文件。

2. 以管理员身份打开命令提示符窗口。 然后，输入以下命令来验证驱动程序是否已按预期签名。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; SignTool verify Echo.Sys</code></pre></td>
   </tr>
   </tbody>
   </table>

3. 若要列出其他信息，并让 signtool 验证包含多个签名的文件中的所有签名，请键入以下命令。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; SignTool verify /pa /ph /v /d Echo.Sys</code></pre></td>
   </tr>
   </tbody>
   </table>

4. 若要确认驱动程序的 EKU，请完成以下步骤。

   a. 打开 Windows 资源管理器并找到二进制文件。 右键单击该文件并选择“属性”。

   b. 在“数字签名”选项卡上，选择“签名列表”中列出的项。

   c. 选择“详细信息”按钮，然后选择“查看证书”。

   d. 在“详细信息”选项卡上，选择“增强型密钥用法”字段。

当驱动程序由仪表板重新签名时，使用以下过程。

-   附加 Microsoft SHA2 嵌入式签名。
-   如果客户使用自己的证书对驱动程序二进制文件进行嵌入式签名，将不会覆盖这些签名。
-   创建新的目录文件并使用 SHA2 Microsoft 证书对该目录文件签名。 该目录会替换客户提供的任何现有目录。

## <a name="span-idtestyourdriveronwindows10fordesktopspanspan-idtestyourdriveronwindows10fordesktopspanspan-idtestyourdriveronwindows10fordesktopspantest-your-driver-on-windows-10-for-desktop"></a><span id="Test_your_driver_on_Windows_10_for_Desktop"></span><span id="test_your_driver_on_windows_10_for_desktop"></span><span id="TEST_YOUR_DRIVER_ON_WINDOWS_10_FOR_DESKTOP"></span>在 Windows 10 桌面版上测试驱动程序


使用以下说明安装示例驱动程序。

1. 打开设备管理器、右键单击计算机图标，然后选择“添加过时硬件”。 按照提示完成驱动程序的安装。

2. 或者，以管理员身份打开“命令提示符”窗口并使用 devcon 安装驱动程序。 导航到你的驱动程序包文件夹，然后输入以下命令。

   <span codelanguage=""></span>
   <table>
   <colgroup>
   <col width="100%" />
   </colgroup>
   <tbody>
   <tr class="odd">
   <td align="left"><pre><code>C:\Echo&gt; devcon install echo.inf root\ECHO</code></pre></td>
   </tr>
   </tbody>
   </table>

3. 确认驱动程序安装过程不会显示“Windows 无法验证该驱动程序软件的发布者。” “Windows 安全”对话框。

## <a name="span-idcreateamultipledriversubmissionspanspan-idcreateamultipledriversubmissionspanspan-idcreateamultipledriversubmissionspancreate-a-multiple-driver-submission"></a><span id="Create_a_Multiple_Driver_Submission"></span><span id="create_a_multiple_driver_submission"></span><span id="CREATE_A_MULTIPLE_DRIVER_SUBMISSION"></span>创建多个驱动程序提交


若要同时提交多个驱动程序，请为每个驱动程序创建一个子目录，如下所示。

![Cab 提交的目录结构](images/b-wes-driversigning-v4.png)

准备将引用子目录的 cab 文件 DDF 输入文件。 它可能如下所示。

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

若要签名、提交和测试驱动程序文件，请按照上述步骤操作。
## 



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [签署驱动程序](signing-a-driver.md)





