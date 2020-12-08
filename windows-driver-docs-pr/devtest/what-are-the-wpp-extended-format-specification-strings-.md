---
title: 什么是 WPP 扩展格式规范字符串
description: 什么是 WPP 扩展格式规范字符串
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0626734ff2d2f92ec64f92dba62bffc11e0c7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810713"
---
# <a name="what-are-the-wpp-extended-format-specification-strings"></a>什么是 WPP 扩展格式规范字符串

WPP 包括预定义格式规范字符串，你可以在跟踪消息中使用这些字符串，此外还可以使用为 **printf** 定义的标准格式字符串。

可以使用 **%！标志！**， **%！FUNC！** **%！LEVEL！** [跟踪消息前缀](trace-message-prefix.md)和任何跟踪函数或宏（如 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))）中的字符串。

可以在任何跟踪函数中使用其他扩展字符串。

|格式字符串|说明|
|----|----|
|**软件跟踪**| |
|%!文件!|显示从中生成跟踪消息的源文件的名称。 此变量还可用于 [跟踪消息前缀](trace-message-prefix.md)|.
|%!随意!|显示启用跟踪消息的 [跟踪标志](trace-flags.md) 的值。 此变量还可以用在  [跟踪消息前缀](trace-message-prefix.md)中。|
|%!求!|显示生成跟踪消息的函数。 此变量还可以用在 [跟踪消息前缀](trace-message-prefix.md)中。|
|%!调配!|显示启用跟踪消息的 [跟踪级别](trace-level.md)  的名称。 此变量还可以用在 [跟踪消息前缀](trace-message-prefix.md)中。|
|%!内嵌!|显示生成跟踪前缀的代码行的行号。 此变量还可以用在 [跟踪消息前缀](trace-message-prefix.md)中。|
|**常规使用**| |
|%！ bool！|显示 TRUE 或 FALSE|
|%！ irql！|显示当前 IRQL 的名称。|
|%！ sid！|表示指向 (pSID) 的安全标识符的指针。 显示 SID。|
|%!SRB!|表示指向 SCSI 请求块的指针。 显示块内容。|
|%!SENSEDATA!|表示指向 SCSI SENSE_DATA 的指针。 显示探测数据。|
|**Guid**| |
|%!GUID.EMPTY!|表示指向 GUID (pGUID) 的指针。 显示指向的 GUID。|
|%!CLSID!|类 ID。 表示指向类 ID GUID 的指针。 显示与 GUID 关联的字符串。 当设置跟踪消息的格式时，WPP 会在注册表中查找字符串。|
|%!IID!|接口 ID。 表示指向接口 ID GUID 的指针。 显示与 GUID 关联的字符串。 当设置跟踪消息的格式时，WPP 会在注册表中查找字符串。|
|%!LIBID!|类型库。 表示 COM 类型库的 GUID。 显示与 GUID 关联的字符串。 当设置跟踪消息的格式时，WPP 会在注册表中查找字符串。|
|**时间**| |
|%！ delta！|显示两个时间值之间的差异（以毫秒为单位）。 它是一个 LONGLONG 值，它以 **日期 ~ h:m： s** 格式显示。|
|%!WAITTIME!|显示等待完成内容所用的时间（以毫秒为单位）。 它是一个 LONGLONG 值，它以 **日期 ~ h:m： s** 格式显示。 旨在与 **%！到期！** 一起使用。|
|%！到期！|显示预计需要完成的时间（以毫秒为单位）。 它是一个 LONGLONG 值，它以 **日期 ~ h:m： s** 格式显示。 设计用于 **%！WAITTIME！**。|
|%!标志! </br>%！ datetime！ </br> %！ time！|显示特定时刻系统时间的值。 它们是以 SYSTEMTIME 格式显示的 LARGE_INTEGER 值。</br>您可以使用这些变量在您的程序中表示不同的时间值，并区分它们。|
|**返回代码**| |
|%!状态值!|表示状态值并显示与状态代码关联的字符串。|
|%!WINERROR.H!|表示一个 Windows 错误代码，并显示与该错误关联的字符串。|
|%!HRESULT!|表示错误或警告，并以 HRESULT 格式显示代码。|
|%!NTerror!|表示 Windows 错误并显示错误消息字符串。|
|**Network**| |
|%!IPADDR!|表示指向 IP 地址的指针。 显示 IP 地址。|
|%!口!|显示端口号。|
|%!NETEVENT!|显示网络事件。|
