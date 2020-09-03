---
title: 如何实现创建自定义 WPP 扩展格式规范字符串
description: 如何实现创建自定义 WPP 扩展格式规范字符串
ms.assetid: 6c4c47c6-71b2-48a0-bab3-8498029b8244
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e0fc783d19b7b08490d841dd027308973a876b7
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383435"
---
# <a name="how-do-i-create-custom-wpp-extended-format-specification-strings"></a>如何创建自定义的 WPP 扩展格式规范字符串？


您可以使用 DEFINE \_ CPLX TYPE 宏创建自定义 WPP 扩展格式规范字符串 \_ 。 有关如何使用此宏的详细信息，请参阅 [复杂类型定义的语法是什么？](what-is-the-syntax-of-the-complex-types-definition-.md)。

本主题提供的示例演示如何执行以下操作：

- [通过自定义 WPP 扩展格式规范字符串跟踪固定长度的字符串](#trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings)

- [通过自定义 WPP 扩展格式规范字符串跟踪可变长度字符串](#trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings)

其中每个示例演示如何将自定义 WPP 配置文件用于定义 \_ CPLX \_ 类型宏的定义。 在这些示例中，配置文件的名称为 LocalWpp.ini。 有关如何使用自定义 WPP 配置文件的详细信息，请参阅 [如何定义自定义数据类型？](how-do-you-define-custom-data-types-.md)。

## <a name="trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings"></a>通过自定义 WPP 扩展格式规范字符串跟踪固定长度的字符串

此示例演示如何使用自定义 WPP 扩展格式规范字符串跟踪 Internet 协议版本 6 (IPv6) 网络地址。 In6 地址结构定义的 IPv6 网络地址的 \_ 长度固定为16字节。

在此示例中，定义了一个 (IPV6ADDR) 的复杂数据类型，然后可以将其用作%！IPV6ADDR! 源代码中的格式规范字符串。

若要创建 IPV6ADDR 复杂数据类型，请将以下语句添加到 LocalWpp.ini 配置文件：

1.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>DEFINE_CPLX_TYPE(IPV6ADDR, WPP_LOGIPV6, in6_addr *, ItemIPV6Addr, "s", _IPV6_, 0, 1);</code></pre></td>
    </tr>
    </tbody>
    </table>

    此语句使用 DEFINE \_ CPLX \_ TYPE 宏定义复杂类型 (IPV6ADDR) 及其属性（如其参数类型 (in6 \_ 地址 \*) 和大小 (16) 。

    语句还指定了 \_ 当 wpp 预处理器在 [跟踪提供程序](trace-provider.md)的源代码中分析 IPV6ADDR 复杂类型时使用的 HELPER 宏 (wpp LOGIPV6) 的名称。

2.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>WPP_FLAGS(-DWPP_LOGIPV6(x) WPP_LOGPAIR( (16), (x)));</code></pre></td>
    </tr>
    </tbody>
    </table>

    此语句定义了 helper 宏，该宏用于在将 IPV6 参数传递到 [TraceMessage](/windows/win32/api/evntrace/nf-evntrace-tracemessage) 函数时设置其长度/地址对的格式。

在 Visual Studio 中，打开项目的 "属性" 页。 在 " **WPP 跟踪**、 **文件选项**" 下，指定 LocalWpp.ini 作为 **附加配置文件**。 有关详细信息，请参阅 [WPP 预处理器](wpp-preprocessor.md) 。

下面的示例代码演示 [跟踪提供程序](trace-provider.md) 如何使用%！IPV6ADDR! 格式规范字符串：

```
struct in6_addr IPAddressV6 = {0};
DoTraceMessage(Noise, "IN6_ADDR  = %!IPV6ADDR!", &IPAddressV6);
```

**注意**   可以创建复杂类型 (MACADDR) ，以跟踪固定长度的媒体访问控制 (MAC) 地址。 可以按照用于 IPV6ADDDR 复杂类型的过程来指定此复杂类型。

 

## <a name="trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings"></a>通过自定义 WPP 扩展格式规范字符串跟踪可变长度字符串

此示例演示如何使用自定义 WPP 扩展格式规范字符串跟踪数据的可变长度缓冲区。

在此示例中，定义了一个 (HEXDUMP) 的复杂数据类型，可以将其用作%！HEXDUMP! 源代码中的格式规范字符串。

若要创建 HEXDUMP 复杂数据类型，请将以下语句添加到 LocalWpp.ini 配置文件：

1.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>DEFINE_CPLX_TYPE(HEXDUMP, WPP_LOGHEXDUMP, const xstr_t&, ItemHEXDump,"s", _HEX_, 0, 2);</code></pre></td>
    </tr>
    </tbody>
    </table>

    此语句使用 DEFINE \_ CPLX \_ TYPE 宏定义复杂类型 (HEXDUMP) 及其属性（如其参数类型 (const xstr \_ t&) 和传递到 **TraceMessage** (2) 的参数的数目。 由于此复杂类型将用于可变长度数据，因此宏的 **Size** 元素设置为零。

    语句还指定了 \_ 当 wpp 预处理器在 [跟踪提供程序](trace-provider.md)的源代码中分析 HEXDUMP 复杂类型时使用的 HELPER 宏 (wpp LOGHEXDUMP) 的名称。

2.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>struct xstr_t {
       CHAR * _buf;
       short _len;
       xstr_t(__in_ecount(len) char *buf, short len):_buf(buf),_len(len) {}
    };</code></pre></td>
    </tr>
    </tbody>
    </table>

    此语句定义用于保存可变长度缓冲区的长度和地址的结构。 此结构在 LOG LENSTR 宏中进行初始化 \_ ，在每次调用 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) 时都是本地的，在这种情况下，在 " *格式字符串* " 参数中使用 HEXDUMP 复杂类型。

3.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>WPP_FLAGS(-DLOG_LENSTR(len,str)=xstr_t(str,len));</code></pre></td>
    </tr>
    </tbody>
    </table>

    此语句定义用于初始化 \_ 可变长度缓冲区的 xstr t 结构的宏。 必须使用此宏在[**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))的*VariableList*参数中传递长度可变的缓冲区。

4.  <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>WPP_FLAGS(-DWPP_LOGHEXDUMP(x) WPP_LOGPAIR(2,&(x)._len) WPP_LOGPAIR((x)._len, (x)._buf));</code></pre></td>
    </tr>
    </tbody>
    </table>

    此语句定义了 helper 宏，该宏用于在将可变长度缓冲参数传递到 [TraceMessage](/windows/win32/api/evntrace/nf-evntrace-tracemessage) 函数时设置其长度/地址对的格式。

    可变长度参数需要两个长度/地址对。 因此，WPP \_ LOGHEXDUMP 宏会按以下方式定义对 WPP LOGPAIR 的两个调用 \_ ：

    -   对 WPP LOGPAIR 的第一次调用会 \_ 传递变长缓冲区的大小。
    -   对 WPP LOGPAIR 的第二次调用会 \_ 传递缓冲区本身的地址。

    **注意**   此宏要求 \_ 通过调用日志 LENSTR 为长度可变的缓冲区初始化 xstr t 结构 \_ 。 因此，必须通过 LOG LENSTR 宏将可变长度缓冲区传递到 [**DoTraceMessage**](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)) \_ 。

     

在 Visual Studio 中，打开项目的 "属性" 页。 在 " **WPP 跟踪**、 **文件选项**" 下，指定 LocalWpp.ini 作为 **附加配置文件**。 有关详细信息，请参阅 [WPP 预处理器](wpp-preprocessor.md) 。

下面的示例代码演示了 [跟踪提供程序](trace-provider.md) 如何使用%！HEXDUMP! 格式规范字符串：

```
CHAR HexDump[1024] = {0, 1, 2, 3, 4, 5, 6, 7} ;
DoTraceMessage(Noise, "HEXDUMP: %!HEXDUMP! ", LOG_LENSTR(sizeof(HexDump),(PCHAR)HexDump));
```

**注意**   可以创建复杂类型 (HEXBYTES) 用于跟踪长度可变的缓冲区。 可以按照用于 HEXDUMP 复杂类型的过程来指定此复杂类型。 