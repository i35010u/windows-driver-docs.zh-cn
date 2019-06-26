---
title: 排查 KMDF 和 UMDF 驱动程序安装问题
description: 排查 KMDF 和 UMDF 驱动程序安装问题
ms.assetid: b0b71adc-cb6e-4b84-a5bf-bd1269bcf315
keywords:
- 内核模式驱动程序框架 WDK，安装驱动程序
- 基于框架的驱动程序 WDK KMDF，安装
- INF 文件 WDK KMDF，调试
- 调试驱动程序 WDK KMDF，安装
- 调试 WDK KMDF 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feece70c877750a49b073899156b711c97c6f803
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377481"
---
# <a name="troubleshooting-kmdf-and-umdf-driver-installation"></a>排查 KMDF 和 UMDF 驱动程序安装问题


框架的共同安装程序会创建调试消息。 如果您正在运行的 Windows 内部的版本，您可以看到这些消息在调试器中。

此外，辅助安装程序将写入到其调试消息[安装程序操作日志](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi-text-logs)( *%windir%\\setupact.log*) 文件。 安装程序操作日志包含共同安装程序和驱动程序的 INF 文件中指定的驱动程序的版本。 您应该验证这些按预期方式。

## <a name="examining-kmdf-installation"></a>检查 KMDF 安装


在安装程序操作日志中输出，下面是从 KMDF 驱动程序成功安装：

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

在上述情况中，不会更新为必要因为在磁盘和内存中的框架版本是 KMDF 1.9，共同安装程序的版本相同。

请考虑以下输出，其中详细介绍了安装失败：

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

在此方案中，更新和重新启动是必要由于内存中版本和 KMDF 运行时的磁盘上的版本早于版本的共同安装程序。 但是，此更新未成功。 辅助安装程序指向其他日志文件在哪里可以找到有关失败的详细信息。

此外可以检查系统事件日志与动态绑定到运行时库的 KMDF 驱动程序相关的错误。 此类错误可能会生成**Wdf**&lt;*MajorVersionNumber*&gt;&lt;*MinorVersionNumber* &gt;中的条目系统事件日志。 在这种情况下，重新启动计算机。 您也可以通过删除强制 KMDF 运行时重新安装**Wdf**&lt;*MajorVersionNumber*&gt;&lt;*MinorVersionNumber*&gt; **.sys**从 *%windir%\\system32\\驱动程序*文件夹。

## <a name="examining-umdf-installation"></a>检查 UMDF 安装


安装程序操作日志中输出以下内容说明了 UMDF 驱动程序安装成功。

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

在上述情况中，不会更新是必要的这是因为运行时的磁盘上的版本是 UMDF 1.9 与共同安装程序的版本相同。

请考虑以下输出，其中详细介绍了安装失败。

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

在此方案中，UMDF 运行时的磁盘上的版本早于版本的共同安装程序。 但是，在这种情况下更新未成功。 辅助安装程序指向额外的日志文件在哪里可以找到有关失败的原因的详细信息。









