---
title: WDI TLV 转储器
description: 分析器生成器库包含将 TLV 字节数组解码为跟踪语句的例程。
ms.assetid: 4F8B53E5-1F51-4119-AC06-7A710340E4A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88cbfdefeee3f0e5c0bbfae2894c28492b5f75cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834104"
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

如果只需要 WPP 跟踪，请使用跟踪 Api，因为它们经过了优化，从而对代码大小和日志大小（ETL 文件中的字符串更少）的影响最小。 如果需要更通用的转储器，可使用转储 Api，因为它们包括 WPP 跟踪，还包括回调例程。 存根（stub）驱动程序提供了一个示例，该示例使用此回调例程将输出重定向到内核调试器（通过 DebugPrint Api）。

与分析和生成 Api 不同，转储器非常强大。 无论给定消息或 TLV 的规范形式如何，它都会尝试充分理解 TLV 字节。 这意味着转储器可能会正确地解码和转储分析器拒绝的内容。

**警告**  如果转储器成功地将字节解码为可读格式，则它并不意味着字节是格式正确的 TLV。

 

与分析 Api 一样， *pBuffer*指针和*BufferLength*参数应该排除任何标头，直接在第一个 TLV 上指向。

Api 的消息变体包括消息 ID 和消息方向，以更好地消除 TLV 的歧义。 这很有用，因为可以根据上下文以不同的方式对同一 TLV ID 进行解码。 例如， [**WDI\_TLV\_BSSID**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bssid)可以直接包含[**WDI\_mac\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)（当 OID 的一部分[\_WDI\_TASK\_扫描](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-scan)时），或者它可以包含**WDI\_MAC 的列表\_** 当 WDI 的一部分[ **\_TLV\_P2P\_属性**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-attributes)时进行寻址。

 

 





