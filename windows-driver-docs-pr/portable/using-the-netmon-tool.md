---
Description: '网络监视器工具 ( # A0) 是一个基于 Windows 的应用程序，可用于从 WPD 组件查看跟踪。'
title: 使用网络监视器工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f9af2b92fcc72c5d3a17a0a5d1b5bd0cb67ff89
ms.sourcegitcommit: e0bec5347825e04fb3b2309d04156b01a83fa593
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88090125"
---
# <a name="using-the-network-monitor-tool"></a>使用网络监视器工具

网络监视器工具 (*NetMon.exe*) 是一个基于 Windows 的应用程序，可用于从 WPD 组件查看跟踪。 该工具替换*WpdMon.exe* ，并提供一种在 Windows 8 中收集和查看 WPD 跟踪的新方法。

## <a name="installing-and-configuring-netmonexe"></a>安装和配置 NetMon.exe

若要安装和配置网络监视器工具，请完成以下步骤。

1. 下载并安装[*NetMon.exe*](https://go.microsoft.com/fwlink/p/?linkid=248501)。
2. 下载并安装[Windows 驱动程序工具包](https://go.microsoft.com/fwlink/p/?linkid=178709)。
3. 通过使用*管理员*权限启动*Powershell.exe*实例并运行以下命令序列，在开发计算机上安装 WPD 分析器。
   1. PowerShell-Set-executionpolicy RemoteSigned
   2. cd " \\ Program Files (x86) \\ Windows 工具包 \\ 8.0 \\ Tools \\ x86 \\ 网络监视器分析器 \\ usb"
   3. ..\\NplAutoProfile.ps1
   4. cd。 \\wpd
   5. ..\\NplAutoProfile.ps1**注意**，    WPD 分析程序包含在 Windows 驱动程序工具包中。

4. 使用 "工具/选项" 对话框配置*NetMon.exe*选项：
   1. 在 "**常规**" 选项卡中，选择 "**在帧摘要中使用固定宽度字体**" 框。
   2. 在 "**颜色规则**" 选项卡中，选择 "**打开**"，然后选择 " \\ 程序文件" (x86) \\ Windows 工具包 \\ 8.0 \\ Tools \\ x86 \\ 网络监视器 \\ wpd \\ wpd. nmcr。 选择 "**打开**"，然后选择 **"确定"。**

完成这些步骤后， *NetMon.exe*准备好检查 WPD 跟踪文件。 若要开始收集跟踪，请按照下一节收集跟踪中的说明进行操作。

## <a name="collecting-traces"></a>收集跟踪

若要生成跟踪，需要创建命令脚本。 将以下内容复制到文本文件，并使用 .cmd 文件扩展名保存该文件。

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

创建命令文件后，从提升的命令会话在 Windows 8 计算机上运行它。

如果使用了示例命令文件的内容，则跟踪将存储在文件 wpd 中 \_ 。

## <a name="viewing-traces"></a>查看跟踪

若要查看跟踪，请启动*NetMon.exe*，选择 "文件"/"打开"/"捕获" 菜单，并打开 \_ 上面收集的 wpd trace .etl 文件。 打开跟踪文件时，您将看到 NetMon.exe 显示不同层的跟踪：

- WPDAPI –通过 WPD 命令和响应显示 WPD API 级别的信息
- WPDMTP –用 MTP 命令和响应显示 MTP 级别的信息
- 传输 (WPDMTPUS 或 WPDMTPIP 或 WPDMTPBT) –显示传输级别数据包

下图显示了 API 级别的 WPDAPI 请求。 请求以 MTP 请求的形式传播 (s) ，该请求将到达传输，然后向上冒泡。

![查看跟踪](images/framesummary1.png)

- 传输级日志记录在数据阶段不记录实际数据。 检查在**GetDeviceInfo**或**SendObjectPropList**等命令期间发送或接收的数据集的 WPDMTP 响应消息。
- 如果在 "**帧摘要**" 窗口中选择 WPDMTP 响应行，则相应的项将在 "**帧详细信息**" 窗口中展开。
- 选择 "**帧详细信息**" 窗口中的 "+" 以进一步展开并浏览。 如果 MTP 操作具有 dataphase，则从设备接收的数据集将在 WPDMTP 响应项的**DataSetOfDataPhase**字段下提供。

![查看跟踪](images/framedetails1.png)

- 您可以选择展开这些项，并看到 "**帧详细信息**" 窗口显示 WPD/MTP 友好消息。 编写 WPD 分析器时遵循的约定是，你将能够在标头级别查看详细信息摘要。 例如，在 GetServiceCapabilities 调用中， **DataSetOfDataPhase**字段显示在它的旁边，这是该数据集中的格式数。
- 您可以删除 "**帧摘要**" 窗口中的 "**源**" 和 "**目标**" 列以提高清晰度
- 在 "**帧详细信息**" 窗口中选择字段时，会在 "**十六进制详细信息**" 窗口中突出显示相应的值。

## <a name="filtering-with-netmonexe"></a>用 NetMon.exe 进行筛选

网络监视器工具提供多个筛选功能。

- 若要仅显示 MTP 跟踪，请在 "**显示筛选器**" 窗口中输入 **！ wpdmtp** ，然后选择 "**应用**"。
- 筛选驱动程序返回错误的情况：
  - 在 "**显示筛选器**" 窗口中输入**wpderror！ = 0** ，然后选择 "**应用**"。
- 可以筛选给定方案的所有方法调用。 例如，以下筛选器将检索对 GetServiceProperties 的所有调用：

    WPDMTP.CorrespondingCommand. MTPOpcode = = 0x9304

- 同样，以下筛选器将检索相同的方法调用：

    WPDMTP.CorrespondingCommand. MTPOpcode = = MTP \_ 操作码 \_ GETSERVICEPROPERTIES
