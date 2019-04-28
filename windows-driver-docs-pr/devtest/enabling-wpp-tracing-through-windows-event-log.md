---
title: 如何启用 WPP 跟踪通过 Windows 事件日志服务
description: Windows 事件日志服务支持 WPP 日志记录和解码。 本主题介绍如何启用通过 Windows 事件日志服务 WPP 跟踪。
ms.assetid: cd5dad3e-fa25-4ec2-bc17-9332b4c00d17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c69c960cf71a05aa6b540360aa1667254160608b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344831"
---
# <a name="how-do-i-enable-wpp-tracing-through-the-windows-event-log-service"></a>如何通过 Windows 事件日志服务启用 WPP 跟踪？


Windows 事件日志服务支持 WPP 日志记录和解码。 本主题介绍如何启用通过 Windows 事件日志服务 WPP 跟踪。

在此方案中的跟踪启用 WPP 需要 WPP 提供程序没有额外工作。 但是，若要使用 Windows 事件日志服务，必须提供一个清单和事件日志提供程序。 若要启用 WPP 跟踪，请声明调试通道，并指定关联的控件所声明的方式为 WPP 提供商的 GUID。

例如：

```xsd
<instrumentationManifest
    xmlns="http://schemas.microsoft.com/win/2004/08/events" 
    xmlns:win="http://manifests.microsoft.com/win/2004/08/windows/events"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema"  xsi:schemaLocation="http://schemas.microsoft.com/win/2004/08/events eventman.xsd"  
    >
   <instrumentation>
        <events>
            <provider name="Microsoft-Windows-mySampleProvider" 
                guid="{61CE3EC9-E5E8-4b96-A451-74631A6E0D5C}" 
                >
          <channel
        chid="MS_WINDOWS_GE_DEBUG"
        enabled="false"
        isolation="System"
        message="$(string.Microsoft-Windows-GenerateEvent.channel.CHANNEL_DEBUG.message)"
        name="Microsoft-Windows-GenerateEvent/Debug"
        symbol="CHANNEL_DEBUG"
        type="Debug"
        >
        <publishing>
          <level>2</level>
          <keywords>0xFFFFFFFF</keywords>
          <controlGuid>{d58c126f-b309-11d1-969e-0000f875a5bc}</controlGuid>
        </publishing>
        </channel>
       </provider>
    </events>
   </instrumentation>
</instrumentationManifest>
```

WPP 跟踪不应启用所有的时间，因此默认情况下**启用**清单中的属性应设置为 false。 当需要 WPP 跟踪时，更改在清单中，该属性，以便**已启用 ="true"**。

不能指定，也可以单独选择控制位。 若要启用所有 WPP 事件到此频道，请指定关键字值为 0XFFFFFFFF。 在内部，控制 bits 一映射到关键字;如果您知道哪一段映射到特定的关键字，则可以选择该关键字来获取一组特定的事件。 示例清单中的关键字值是 0xFFFF，因为所需少于 16 个 WPP 控制位。 若要安装完成后获取一组特定的事件，可能会更改使用 wevtutil.exe 命令行实用工具的关键字。 命令为：

**wevtutil** **sl** *&lt;通道名称&gt;***/k:***&lt;对应于控制位的关键字值&gt;*

请注意，通道必须先禁用更改的关键字值。

声明这种方式中的通道使 WPP 提供程序 （其控制指定 GUID） 和事件日志提供程序 （在此通道声明的） 访问调试通道，因此哪种提供程序可以写入此通道。 现在可以下此通道通过事件查看器查看 WPP 事件或普通的 ETW 事件。

未解码 WPP 事件。 若要获取与这些事件关联的消息字符串，请将 TMF 文件放在 %windir%\\System32\\winevt\\TraceFormat 目录。 可以通过使用 Tracepdb.exe，它将输入 PDB 文件并返回 TMF 文件之类的实用工具获取 TMF 文件。

 

 





