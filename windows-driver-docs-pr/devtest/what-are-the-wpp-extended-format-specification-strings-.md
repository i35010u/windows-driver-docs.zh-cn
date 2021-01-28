---
title: 什么是 WPP 扩展格式规范字符串
description: 什么是 WPP 扩展格式规范字符串
ms.date: 01/27/2021
ms.localizationpriority: medium
ms.openlocfilehash: 40759e14737763d68bfaeefa4ce89bf3c8711b0a
ms.sourcegitcommit: 468156fa76f3740f843cf503d57a68b92d548f7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "98949237"
---
# <a name="what-are-the-wpp-extended-format-specification-strings"></a>什么是 WPP 扩展格式规范字符串

WPP 包括预定义格式规范字符串，你可以在跟踪消息中使用这些字符串，此外还可以使用为 **printf** 定义的标准格式字符串。

可以使用 **%！标志！**， **%！FUNC！** **%！LEVEL！** [跟踪消息前缀](trace-message-prefix.md)和任何跟踪函数或宏（如 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))）中的字符串。

可以在任何跟踪函数中使用其他扩展字符串。

## <a name="default-configuration-options-for-tracewpp"></a>Tracewpp 的默认配置选项

WPP 使用 "defaultwpp.ini" 作为默认配置设置。 此默认 INI 文件作为 Windows SDK 的一部分包含在 WppConfig 4.1 目录中。 有关 WPP 默认行为的最新信息以及有关自定义的其他信息，请参阅此 INI 文件。

### <a name="software-tracing"></a>软件跟踪

|格式字符串|说明|
|----|----|
|%!文件!|显示从中生成跟踪消息的源文件的名称。 此变量还可用于 [跟踪消息前缀](trace-message-prefix.md)|.
|%!随意!|显示启用跟踪消息的 [跟踪标志](trace-flags.md) 的值。 此变量还可以用在  [跟踪消息前缀](trace-message-prefix.md)中。|
|%!求!|显示生成跟踪消息的函数。 此变量还可以用在 [跟踪消息前缀](trace-message-prefix.md)中。|
|%!调配!|显示启用跟踪消息的 [跟踪级别](trace-level.md)  的名称。 此变量还可以用在 [跟踪消息前缀](trace-message-prefix.md)中。|
|%!内嵌!|显示生成跟踪前缀的代码行的行号。 此变量还可以用在 [跟踪消息前缀](trace-message-prefix.md)中。|

### <a name="general-use"></a>常规使用

|格式字符串|说明|
|----|----|
|%！ bool！|显示 TRUE 或 FALSE|
|%！ irql！|显示当前 IRQL 的名称。|
|%！ sid！|表示指向 (pSID) 的安全标识符的指针。 显示 SID。|
|**Guid**| |
|%!GUID.EMPTY!|表示指向 GUID (pGUID) 的指针。 显示指向的 GUID。|
|%!CLSID!|类 ID。 表示指向类 ID GUID 的指针。 显示与 GUID 关联的字符串。 当设置跟踪消息的格式时，WPP 会在注册表中查找字符串。|
|%!LIBID!|类型库。 表示 COM 类型库的 GUID。 显示与 GUID 关联的字符串。 当设置跟踪消息的格式时，WPP 会在注册表中查找字符串。|
|%!IID!|接口 ID。 表示指向接口 ID GUID 的指针。 显示与 GUID 关联的字符串。 当设置跟踪消息的格式时，WPP 会在注册表中查找字符串。|
|**时间**| |
|%！ delta！|显示两个时间值之间的差异（以毫秒为单位）。 它是一个 LONGLONG 值，它以 **日期 ~ h:m： s** 格式显示。|
|%!WAITTIME!|显示等待完成内容所用的时间（以毫秒为单位）。 它是一个 LONGLONG 值，它以 **日期 ~ h:m： s** 格式显示。 旨在与 **%！到期！** 一起使用。|
|%！到期！|显示预计需要完成的时间（以毫秒为单位）。 它是一个 LONGLONG 值，它以 **日期 ~ h:m： s** 格式显示。 设计用于 **%！WAITTIME！**。|
|%!标志! </br>%！ datetime！ </br> %!阶段!|显示特定时刻系统时间的值。 这些是以 SYSTEMTIME 格式显示的 LONGLONG (SINT64) 值。</br>您可以使用这些变量在您的程序中表示不同的时间值，并区分它们。|

### <a name="return-codes"></a>返回代码

|格式字符串|说明|
|----|----|
|%!状态值!|表示状态值并显示与状态代码关联的字符串。|
|%!WINERROR.H!|表示一个 Windows 错误代码，并显示与该错误关联的字符串。|
|%!HRESULT!|表示错误或警告，并以 HRESULT 格式显示代码。|

### <a name="network"></a>网络
|格式字符串|说明|
|----|----|
|%!IPADDR!|表示指向 IP 地址的指针。 显示 IP 地址。|
|%!口!|显示端口号。|
