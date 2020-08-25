---
title: 如何通过 Windows 事件日志服务启用 WPP 跟踪
description: Windows 事件日志服务支持 WPP 日志记录和解码。 本主题介绍如何通过 Windows 事件日志服务启用 WPP 跟踪。
ms.assetid: cd5dad3e-fa25-4ec2-bc17-9332b4c00d17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cc25245b0eb4248c2a531e2e1e39218b80df6d9
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802739"
---
# <a name="how-to-enable-wpp-tracing-through-the-windows-event-log-service"></a>如何通过 Windows 事件日志服务启用 WPP 跟踪

Windows 事件日志服务支持 WPP 日志记录和解码。 本主题介绍如何通过 Windows 事件日志服务启用 WPP 跟踪。

在这种情况下启用 WPP 跟踪不需要对 WPP 提供程序执行额外的工作。 但是，若要使用 Windows 事件日志服务，必须提供清单和事件日志提供程序。 若要启用 WPP 跟踪，请声明调试通道并指定为 WPP 提供程序声明的关联的控件 GUID。

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

不打算始终启用 WPP 跟踪，因此默认情况下，清单中的 **enable** 特性应设置为 false。 如果需要 WPP 跟踪，请更改清单中的属性，使 **其为 enabled = "true"**。

不能指定或单独选择控制位。 若要启用此通道的所有 WPP 事件，请将关键字值指定为0XFFFFFFFF。 在内部，控制位映射到关键字;如果知道哪个位映射到特定关键字，则可以选择该关键字以获取特定的一组事件。 在示例清单中，关键字值为0xFFFF，因为需要的 WPP 控制位少于16个。 若要在安装后获取一组特定的事件，可以使用 wevtutil.exe 命令行实用程序更改关键字。 命令为：

**wevtutil** **sl** * &lt; 通道名称 &gt; ***/k：*** &lt; 对应于控件位 &gt; 的关键字值*

请注意，必须先禁用通道，才能更改关键字值。

通过以这种方式声明通道，可同时启用 WPP 提供程序 (的控件 GUID) 和事件日志提供程序 (，在该提供程序中将此通道) 声明为访问调试通道，以便提供程序可以写入该通道。 现在，可以通过事件查看器在此通道下显示 WPP 事件或普通 ETW 事件。

不解码 WPP 事件。 若要获取与这些事件关联的消息字符串，请将 TMF 文件放在% windir% \\ System32 \\ winevt \\ TraceFormat 目录中。 你可以使用诸如 Tracepdb.exe 的实用工具获取 TMF 文件，这会将 PDB 文件用于输入并返回 TMF 文件。
