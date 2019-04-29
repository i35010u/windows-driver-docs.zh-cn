---
Description: 网络监视工具 (NetMon.exe) 是基于 Windows 的应用程序，可用于查看来自 WPD 组件的跟踪。
title: 使用网络监视器工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0de82fbc512572af5f18e1524fe032adbed34a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370471"
---
# <a name="using-the-network-monitor-tool"></a>使用网络监视器工具


网络监视器工具 (*NetMon.exe*) 是一个基于 Windows 的应用程序，可用于查看来自 WPD 组件的跟踪。 该工具将替换*WpdMon.exe* ，并提供新的收集和查看 WPD 跟踪在 Windows 8 中。

## <a name="span-idinstallingandconfiguringnetmonexespanspan-idinstallingandconfiguringnetmonexespaninstalling-and-configuring-netmonexe"></a><span id="installing_and_configuring_netmon.exe"></span><span id="INSTALLING_AND_CONFIGURING_NETMON.EXE"></span>安装和配置 NetMon.exe


若要安装和配置网络监视工具，请完成以下步骤。

1.  下载并安装*NetMon.exe*从[此处](https://go.microsoft.com/fwlink/p/?linkid=248501)。
2.  下载并安装 Windows 驱动程序工具包从[此处](https://go.microsoft.com/fwlink/p/?linkid=178709)。
3.  通过启动的实例在开发计算机上安装 WPD 分析器*Powershell.exe*与*管理员*权限并运行以下命令序列。
    1.  PowerShell -ExecutionPolicy RemoteSigned
    2.  cd"\\Program Files (x86)\\Windows 工具包\\8.0\\工具\\x86\\网络监视器分析器\\usb"
    3.  ..\\NplAutoProfile.ps1
    4.  cd ..\\wpd
    5.  ..\\NplAutoProfile.ps1**注意**  WPD 分析器包含 Windows 驱动程序工具包中。

         

4.  配置*NetMon.exe*通过使用工具/选项对话框的选项：
    1.  在中**常规**选项卡上，选中**帧摘要中的使用固定的宽度字体**框。
    2.  在中**颜色规则**选项卡上，选择**打开**，然后选择\\Program Files (x86)\\Windows 工具包\\8.0\\工具\\x86\\网络监视器分析器\\wpd\\wpd.nmcr。 单击**开放**后, 跟**确定。**

完成这些步骤后*NetMon.exe*已准备好检查 WPD 跟踪文件。 若要开始收集跟踪，请按照下一部分中，收集跟踪。

## <a name="span-idcollectingtracesspanspan-idcollectingtracesspanspan-idcollectingtracesspancollecting-traces"></a><span id="Collecting_Traces"></span><span id="collecting_traces"></span><span id="COLLECTING_TRACES"></span>收集跟踪


若要生成的跟踪，你将需要创建命令脚本。 将以下内容复制到文本文件并将其保存.cmd 文件扩展名。

```cmd
echo off
@REM ---------------------------------------------------------------------------------------
@REM UNCOMMENT THE LOGMAN COMMANDS FOR THE FOLLOWING PROVIDERS AS REQUIRED
@REM Microsoft-Windows-WPD-API                 To log API traffic
@REM Microsoft-Windows-WPD-MTPClassDriver      To log MTP command, response and datasets
@REM Microsoft-Windows-WPD-MTPUS               To log USB traffic at WpdMtpUS layer
@REM Microsoft-Windows-WPD-MTPIP               To log IP traffic at WpdMtpIP layer
@REM Microsoft-Windows-WPD-MTPBT               To log BT traffic at WpdMtpBt layer
@REM Microsoft-Windows-USB-USBPORT             To log USB core layer traffic
@REM Microsoft-Windows-USB-USBHUB              To log USB core layer traffic
@REM ---------------------------------------------------------------------------------------

@REM Start Logging

logman start  -ets WPD -p Microsoft-Windows-WPD-API            -bs 100 -nb 128 640 -o wpd_trace.etl
logman update -ets WPD -p Microsoft-Windows-WPD-MTPClassDriver -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-WPD-MTPUS          -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-WPD-MTPIP          -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-WPD-MTPBT          -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-USB-USBPORT        -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-USB-USBHUB         -bs 100 -nb 128 640
logman update -ets WPD -p Microsoft-Windows-Kernel-IoTrace 0 2
echo. 
echo Please run your scenario now and
pause

@REM Stop logging
logman stop -ets WPD
```

创建命令文件后，请从提升的命令会话在 Windows 8 计算机上运行它。

如果使用的示例命令文件的内容，跟踪将存储在文件 wpd\_trace.etl。

## <a name="span-idviewingtracesspanspan-idviewingtracesspanspan-idviewingtracesspanviewing-traces"></a><span id="Viewing_Traces"></span><span id="viewing_traces"></span><span id="VIEWING_TRACES"></span>查看跟踪内容


若要查看跟踪，请启动*NetMon.exe*，选择文件 / 打开 / 捕获菜单，然后打开 wpd\_trace.etl 文件收集上面。 打开跟踪文件时将看到 NetMon.exe 在各层显示跟踪：

-   WPDAPI – 从 WPD API 级别有 WPD 命令和响应显示信息
-   WPDMTP – 从 MTP 级别与 MTP 命令和响应显示信息
-   传输 （WPDMTPUS 或 WPDMTPIP 或 WPDMTPBT） – 显示传输级别的数据包

下图显示了在 API 级别的 WPDAPI 请求。 请求通过 WPDMTP 传输形式的 MTP 请求到达的传输，然后向上冒泡。

![查看跟踪内容](images/framesummary1.png)

-   传输级日志记录不在数据阶段期间记录的实际数据。 检查 WPDMTP 响应消息的发送或接收的命令，例如期间的数据集**GetDeviceInfo**或**SendObjectPropList**。
-   如果在 WPDMTP 响应行中单击**帧摘要**窗口中，相应的项目中会展开**帧详细信息**窗口。
-   单击中的"+"s**帧详细信息**窗口可以进一步展开和探索。 如果某个 MTP 操作具有 dataphase，从设备收到的数据集位于下**DataSetOfDataPhase** WPDMTP 响应项的字段。

![查看跟踪内容](images/framedetails1.png)

-   您可以单击以展开的项并看到**帧详细信息**窗口会显示 WPD/MTP 友好消息。 编写 WPD 分析器是您将能够查看在标头级别的详细信息的摘要时，将遵循约定。 例如，在 GetServiceCapabilities 调用中， **DataSetOfDataPhase**字段显示下一步，向其中该数据集格式的数字。
-   您可以删除**源**并**目标**中的列**帧摘要**窗口以提高清晰度
-   当您单击中的字段**帧详细信息**窗口中，相应的值中突出显示**Hex 详细信息**窗口。

## <a name="span-idfilteringwithnetmonexespanspan-idfilteringwithnetmonexespanfiltering-with-netmonexe"></a><span id="filtering_with_netmon.exe"></span><span id="FILTERING_WITH_NETMON.EXE"></span>使用 NetMon.exe 进行筛选


网络监视工具提供了多个筛选功能。

-   若要显示仅 MTP 跟踪，请键入 **！ wpdmtp**中**显示筛选器**窗口，然后单击**应用**。
-   若要筛选的情况下，驱动程序返回了一个错误：
    -   类型**wpderror ！ = 0**中**显示筛选器**窗口，然后单击**应用**。
-   您可以筛选所有针对给定方案的方法调用。 例如，以下筛选器会检索所有 GetServiceProperties 对的调用：

    WPDMTP.CorrespondingCommand.MTPOpcode == 0x9304

-   同样地，以下筛选器将检索相同的方法调用：

    WPDMTP.CorrespondingCommand.MTPOpcode == MTP\_OPCODE\_GETSERVICEPROPERTIES

 

 




