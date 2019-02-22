---
title: WDI TLV dumpers
description: 分析器生成器库有例程来解码为跟踪语句的 TLV 字节数组。
ms.assetid: 4F8B53E5-1F51-4119-AC06-7A710340E4A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cee50be2223923c03fa3ebcd1874dd9152f150a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543529"
---
# <a name="wdi-tlv-dumpers"></a>WDI TLV dumpers


分析器生成器库有例程来解码为跟踪语句的 TLV 字节数组。

```C++
    typedef _Function_class_( TlvDumperCallback ) void( __stdcall *TlvDumperCallback )(_In_ UINT_PTR Context, _In_z_ _Printf_format_string_ PCSTR Format, ...);

    void __stdcall TraceUnknownTlvByteStream(
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer );

    void __stdcall TraceMessageTlvByteStream(
        _In_ ULONG MessageId,
        _In_ BOOLEAN fToIhv,
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer );

    void __stdcall DumpUnknownTlvByteStream(
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer,
        _In_opt_ ULONG_PTR Context,
        _In_opt_ TlvDumperCallback pCallback );

    void __stdcall DumpMessageTlvByteStream(
        _In_ ULONG MessageId,
        _In_ BOOLEAN fToIhv,
        _In_ ULONG PeerVersion,
        _In_ ULONG BufferLength,
        _In_reads_bytes_( BufferLength ) UINT8 const * pBuffer,
        _In_opt_ ULONG_PTR Context,
        _In_opt_ TlvDumperCallback pCallback );
```

如果您只需要 WPP 跟踪，因为经过了优化，具有最小影响以代码大小，以及日志大小 （较少字符串 ETL 文件中） 使用跟踪 Api。 如果您需要一种更通用目的转储器，请使用转储 Api，因为它们包括 WPP 跟踪，还包括回调例程。 存根 （stub） 驱动程序存在使用此回调例程将输出重定向到内核调试器通过 DebugPrint Api 的示例。

与不同的分析和生成的 Api，是很宽松转储器。 它会尝试以有意义的 TLV 字节最佳的方式，而不考虑给定的消息或 TLV 的规范格式。 这意味着转储器可能会正确解码和转储的分析程序拒绝。

**警告**  如果转储器已成功将字节解码为人工可读格式，它并不意味着字节是格式正确的 TLV。

 

喜欢分析 Api *pBuffer*指针和*BufferLength*参数应排除任何标头，并直接指向第一个 TLV。

Api 消息变体包括消息 ID 和消息方向以更好地消除歧义 TLV。 这是很有帮助的因为相同的 TLV ID 可以解码不同的方式取决于上下文。 例如， [ **WDI\_TLV\_BSSID** ](https://msdn.microsoft.com/library/windows/hardware/dn926153)可以直接包含[ **WDI\_MAC\_地址**](https://msdn.microsoft.com/library/windows/hardware/dn926071)的一部分时[OID\_WDI\_任务\_扫描](https://msdn.microsoft.com/library/windows/hardware/dn925959)，也可以包含一系列**WDI\_MAC\_地址**的一部分时[ **WDI\_TLV\_P2P\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn897863)。

 

 





