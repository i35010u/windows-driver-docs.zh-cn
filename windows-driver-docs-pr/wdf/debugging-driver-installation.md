---
title: 排查 KMDF 和 UMDF 驱动程序安装问题
description: 排查 KMDF 和 UMDF 驱动程序安装问题
ms.assetid: b0b71adc-cb6e-4b84-a5bf-bd1269bcf315
keywords:
- 内核模式驱动程序框架 WDK，安装驱动程序
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，调试
- 调试驱动程序 WDK KMDF，安装
- 驱动程序调试 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a18a6e70d7fb284d39becef93de0a4feccd07d1c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189171"
---
# <a name="troubleshooting-kmdf-and-umdf-driver-installation"></a>排查 KMDF 和 UMDF 驱动程序安装问题


框架的共同安装程序将创建调试消息。 可以在调试器中查看这些消息。

此外，共同安装程序会将其调试消息写入 [安装操作日志](../install/setupapi-text-logs.md) (*% windir% \\ setupact.log*) 文件中。 安装操作日志包含驱动程序的 INF 文件中指定的共同安装程序和驱动程序的版本。 应该验证这些是否与预期相同。

## <a name="examining-kmdf-installation"></a>检查 KMDF 安装


安装操作日志中的以下输出来自成功安装 KMDF 驱动程序：

```cpp
WdfCoInstaller: DIF_INSTALLDEVICE: Pre-Processing
WdfCoInstaller: ReadComponents:  WdfSection for Driver Service ECHO using KMDF lib version Major 0x1, minor 0x9 
WdfCoInstaller: DIF_INSTALLDEVICE: Coinstaller version: 1.9.7100
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF in-memory version: 1.9.7100
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF on-disk version: 1.9.7100
WdfCoInstaller: Service Wdf01000 is running
WdfCoInstaller: DIF_INSTALLDEVICE: Update is not required. The on-disk KMDF version is newer than or same as the version of the coinstaller
WdfCoInstaller: DIF_INSTALLDEVICE: Post-Processing
```

在上述方案中，不需要进行任何更新，因为磁盘上版本和内存中 framework 版本是 KMDF 1.9，后者是相同版本的共同安装程序。

请考虑以下输出，其中详细说明了不成功的安装：

```cpp
WdfCoInstaller: ReadComponents:  WdfSection for Driver Service ECHO using KMDF lib version Major 0x1, minor 0x9  
WdfCoInstaller: DIF_INSTALLDEVICE: Coinstaller version: 1.9.7100
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF in-memory version: 1.7.6000
WdfCoInstaller: DIF_INSTALLDEVICE: KMDF on-disk version: 1.7.6000
WdfCoInstaller: Service Wdf01000 is running
WdfCoInstaller: DIF_INSTALLDEVICE: Reboot is required, because the in-memory KMDF version is older than the coinstaller's version.
WdfCoInstaller: DIF_INSTALLDEVICE: Update is required, because the on-disk KMDF version is older than the coinstaller
WdfCoInstaller: VerifyMSRoot: exit: error(0) The operation completed successfully.
WdfCoInstaller: Invoking "D:\Windows\system32\wusa.exe "D:\Windows\Temp\WdfTemp\Microsoft Kernel-Mode Driver Framework Install-v1.9-Vista.msu" /quiet /norestart".
WdfCoInstaller: The update process returned error code :error(265) <no error text>. 
WdfCoInstaller: For additional information please look at the log files %windir%\windowsupdate.log and %windir%\Logs\CBS\CBS.log
```

在这种情况下，更新和重新启动都是必需的，因为 KMDF 运行时的内存中版本和磁盘上版本早于共同安装程序的版本。 但是，更新未成功。 共同安装程序将指向其他日志文件，你可以在其中找到有关失败的详细信息。

你还可以检查系统事件日志中是否有与 KMDF 驱动程序的动态绑定相关的错误到运行库。 此类错误可能**Wdf** &lt; *MajorVersionNumber* &gt; &lt; *MinorVersionNumber* &gt; 在系统事件日志中生成 Wdf MajorVersionNumber MinorVersionNumber 项。 在这种情况下，请重新启动计算机。 还可以通过**Wdf** &lt; *MajorVersionNumber* &gt; &lt; *MinorVersionNumber* &gt; **.sys**从 *% windir% \\ system32 \\ 驱动程序*文件夹中删除 Wdf MajorVersionNumber MinorVersionNumber，来强制重新安装 KMDF 运行时。

## <a name="examining-umdf-installation"></a>检查 UMDF 安装


安装操作日志中的以下输出描述了成功的 UMDF 驱动程序安装。

```cpp
WudfUpdate: installing version (1,9,0,7100).
WudfUpdate: Checking for presence of previous UMDF installation.
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfrd.sys version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfpf.sys version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfhost.exe version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfsvc.dll version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfx.dll version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfplatform.dll version (1.9.0.7100)
WudfUpdate: Found binary %WINDIR%\system32\wudfcoinstaller.dll version (1.9.0.7100)
WudfUpdate: UMDF installation is same as update. WudfUpdate: Loading configuration coinstaller from D:\Windows\system32\wudfcoinstaller.dll.
WudfCoInstaller: ReadWdfSection: Checking WdfSection [Echo_Install.NT.Wdf]
WudfCoInstaller: Configuring UMDF Service  WUDFEchoDriver.
WudfCoInstaller: Service WudfSvc is already running.
WudfCoInstaller: Final status: error(0) The operation completed successfully.
```

在上述方案中，不需要进行任何更新，因为运行时版本是 UMDF 1.9，后者与共同安装程序的版本相同。

请考虑以下输出，该输出详细说明了安装不成功。

```cpp
WudfUpdate: installing version (1,9,0,7100).
WudfUpdate: Checking for presence of previous UMDF installation.
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfrd.sys version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\drivers\wudfpf.sys version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfhost.exe version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfsvc.dll version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfx.dll version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfplatform.dll version (1.5.0.6000)
WudfUpdate: Found binary %WINDIR%\system32\wudfcoinstaller.dll version (1.5.0.6000)
WudfUpdate: UMDF installation is older than current.
WudfUpdate: Locating resource stream WUDF_UPDATE_VISTA-RTM.
WudfUpdate: unpacking update from resource to Microsoft User-Mode Driver Framework Install-v1.9-Vista.msu.
WudfUpdate: Temporary path is D:\Windows\Temp\WDF7625.tmp.
WudfUpdate: Invoking update "%SYSTEMROOT%\system32\wusa.exe" with command line "D:\Windows\Temp\WDF7625.tmp\Microsoft User-Mode Driver Framework Install-v1.9-Vista.msu /quiet /norestart".
WudfUpdate: Waiting for update to terminate.
WudfUpdate: Update process returned 22.
WudfUpdate: update returned error 0x16 - error(22) The device does not recognize the command.
WudfUpdate: For additional information please look at the log files %windir%\windowsupdate.log and %windir%\Logs\CBS\CBS.log
WudfUpdate: Cleaning up update.
WudfUpdate: Error updating UMDF - error(22) The device does not recognize the command. Aborting installation.
```

在这种情况下，UMDF 运行时的磁盘版本早于共同安装程序的版本。 但在这种情况下，更新不会成功。 共同安装程序将指向其他日志文件，你可以在其中找到有关失败原因的详细信息。