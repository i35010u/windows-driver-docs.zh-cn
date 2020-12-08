---
title: WDI TLV 转储器
description: 分析器生成器库包含将 TLV 字节数组解码为跟踪语句的例程。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837f16b90c3008491317b9015611344a1234f28b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839865"
---
# <a name="wdi-tlv-dumpers"></a>WDI TLV 转储器


分析器生成器库包含将 TLV 字节数组解码为跟踪语句的例程。

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

如果只需要 WPP 跟踪，请使用跟踪 Api，因为它们经过了优化，从而对代码大小和日志大小的影响最小，这 (ETL 文件) 中的字符串更少。 如果需要更通用的转储器，可使用转储 Api，因为它们包括 WPP 跟踪，还包括回调例程。 存根（stub）驱动程序提供了一个示例，该示例使用此回调例程将输出重定向到内核调试器（通过 DebugPrint Api）。

与分析和生成 Api 不同，转储器非常强大。 无论给定消息或 TLV 的规范形式如何，它都会尝试充分理解 TLV 字节。 这意味着转储器可能会正确地解码和转储分析器拒绝的内容。

**警告**  如果转储器成功将字节解码为可读格式，则它并不意味着字节是格式正确的 TLV。

 

与分析 Api 一样， *pBuffer* 指针和 *BufferLength* 参数应该排除任何标头，直接在第一个 TLV 上指向。

Api 的消息变体包括消息 ID 和消息方向，以更好地消除 TLV 的歧义。 这很有用，因为可以根据上下文以不同的方式对同一 TLV ID 进行解码。 例如，当 [OID \_ WDI \_ 任务 \_ 扫描](./oid-wdi-task-scan.md)的一部分时， [**WDI \_ TLV \_ BSSID**](./wdi-tlv-bssid.md)可以直接包含 [**WDI \_ mac \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)，也可以在 [**WDI \_ TLV \_ P2P \_ 属性**](./wdi-tlv-p2p-attributes.md)中包含 **WDI \_ MAC \_ 地址** 的列表。

 

