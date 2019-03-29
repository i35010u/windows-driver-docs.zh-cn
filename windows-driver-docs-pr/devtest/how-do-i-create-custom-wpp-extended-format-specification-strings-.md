---
title: 如何创建自定义 WPP 扩展的格式规范字符串
description: 如何创建自定义 WPP 扩展的格式规范字符串
ms.assetid: 6c4c47c6-71b2-48a0-bab3-8498029b8244
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4778aab27945662eca2422ae55cb594c516632
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464265"
---
# <a name="how-do-i-create-custom-wpp-extended-format-specification-strings"></a>如何创建自定义的 WPP 扩展格式规范字符串？


通过使用定义创建自定义 WPP 扩展的格式规范字符串\_CPLX\_类型宏。 有关如何使用此宏的详细信息，请参阅[什么是复杂的语法类型定义？](what-is-the-syntax-of-the-complex-types-definition-.md)。

本主题提供了示例，演示如何执行以下操作：

- [跟踪固定长度字符串也可以通过自定义扩展 WPP 格式规范字符串](#trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings)

- [跟踪长度可变的字符串也可以通过自定义扩展 WPP 格式规范字符串](#trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings)

每个示例演示如何使用的定义中定义的自定义 WPP 配置文件\_CPLX\_类型宏。 在这些示例中，配置文件命名为 LocalWpp.ini。 有关如何使用自定义 WPP 配置文件的详细信息，请参阅[如何定义自定义数据类型？](how-do-you-define-custom-data-types-.md)。

## <a name="trace-fixed-length-strings-through-custom-wpp-extended-format-specification-strings"></a>跟踪固定长度字符串也可以通过自定义扩展 WPP 格式规范字符串

此示例演示如何跟踪 Internet 协议版本 6 (IPv6) 网络地址通过使用自定义 WPP 扩展格式规范的字符串。 IPv6 网络地址，由 in6 定义\_addr 结构，具有固定长度长度为 16 个字节。

在此示例中，复杂的数据类型 (IPV6ADDR) 定义，然后用作 %！IPV6ADDR ！ 格式规范在源代码中的字符串。

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

    此语句使用友好名称\_CPLX\_类型宏来定义复杂类型 (IPV6ADDR) 以及其属性，例如其自变量类型 (in6\_addr \*) 和大小 (16)。

    该语句还指定了一个帮助器宏的名称 (WPP\_LOGIPV6) 分析的源代码中的 IPV6ADDR 复杂类型时所使用的 WPP 预处理器你[跟踪提供程序](trace-provider.md)。

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

    此语句定义用于格式化 IPV6 参数的长度/地址对传递给帮助器宏[TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)函数。

在 Visual Studio 中，打开你的项目的属性页。 下**WPP 跟踪**，**文件选项**，指定作为 LocalWpp.ini**额外的配置文件**。 请参阅[WPP 预处理器](wpp-preprocessor.md)有关详细信息。

下面的示例源的代码演示如何在[跟踪提供程序](trace-provider.md)可以跟踪 IPv6 网络地址的通过使用 %！IPV6ADDR ！ 格式规范的字符串：

```
struct in6_addr IPAddressV6 = {0};
DoTraceMessage(Noise, "IN6_ADDR  = %!IPV6ADDR!", &IPAddressV6);
```

**请注意**  跟踪固定长度媒体访问控制 (MAC) 地址，可以创建复杂类型 (MACADDR)。 此复杂类型可以指定用于 IPV6ADDDR 复杂类型的过程。

 

## <a name="trace-variable-length-strings-through-custom-wpp-extended-format-specification-strings"></a>跟踪长度可变的字符串也可以通过自定义扩展 WPP 格式规范字符串

此示例演示如何通过使用扩展格式规范的字符串自定义 WPP 跟踪长度可变的缓冲区的数据。

在此示例中，这可以用作 %定义复杂数据类型 (HEXDUMP) ！HEXDUMP ！ 格式规范在源代码中的字符串。

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

    此语句使用友好名称\_CPLX\_类型宏来定义复杂类型 (HEXDUMP) 以及其属性，例如其自变量类型 (const xstr\_t &) 和数量的参数传递给**TraceMessage** (2)。 由于此复杂类型是要用于长度可变的数据，该宏**大小**元素设置为零。

    该语句还指定了一个帮助器宏的名称 (WPP\_LOGHEXDUMP) 分析的源代码中的 HEXDUMP 复杂类型时所使用的 WPP 预处理器你[跟踪提供程序](trace-provider.md)。

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

    此语句定义的结构，用于保存的长度和可变长度的缓冲区的地址。 在日志中初始化此结构\_LENSTR 宏是每次调用本地[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)在 HEXDUMP 复杂类型在使用*FormatString*参数。

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

    此语句定义的宏，用来初始化 xstr\_t 结构的长度可变的缓冲区。 必须使用此宏将传递在长度可变的缓冲区*VariableList*的参数[ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)。

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

    此语句定义的帮助器宏，用于设置长度可变的缓冲区参数的长度/地址对格式时传递给[TraceMessage](https://go.microsoft.com/fwlink/p/?linkid=179214)函数。

    长度可变的自变量需要两个长度/地址对。 因此，WPP\_LOGHEXDUMP 宏可定义两个调用 WPP\_LOGPAIR 如下所示：

    -   首次调用 WPP\_LOGPAIR 传递长度可变的缓冲区的大小。
    -   第二个调用 WPP\_LOGPAIR 传递的缓冲区本身的地址。

    **请注意**  此宏需要 xstr\_t 结构已初始化，长度可变的缓冲区通过日志调用\_LENSTR。 因此，必须将传递到长度可变的缓冲区[ **DoTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff544918)通过日志\_LENSTR 宏。

     

在 Visual Studio 中，打开你的项目的属性页。 下**WPP 跟踪**，**文件选项**，指定作为 LocalWpp.ini**额外的配置文件**。 请参阅[WPP 预处理器](wpp-preprocessor.md)有关详细信息。

下面的示例源的代码演示如何在[跟踪提供程序](trace-provider.md)可以跟踪数据的缓冲区，使用 %！HEXDUMP ！ 格式规范的字符串：

```
CHAR HexDump[1024] = {0, 1, 2, 3, 4, 5, 6, 7} ;
DoTraceMessage(Noise, "HEXDUMP: %!HEXDUMP! ", LOG_LENSTR(sizeof(HexDump),(PCHAR)HexDump));
```

**请注意**  可以用于跟踪长度可变的缓冲区创建复杂类型 (HEXBYTES)。 此复杂类型可以指定用于 HEXDUMP 复杂类型的过程。 





