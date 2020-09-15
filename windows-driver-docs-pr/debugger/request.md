---
title: IDebugAdvanced2 请求方法
description: 请求方法执行各种不同的操作。
ms.assetid: efb3c93c-5405-418b-a063-afa8e5e9e59a
keywords:
- 请求方法 Windows 调试
- 请求方法 Windows 调试，IDebugAdvanced2 接口
- IDebugAdvanced2 接口 Windows 调试，请求方法
- 请求方法 Windows 调试，IDebugAdvanced3 接口
- IDebugAdvanced3 接口 Windows 调试，请求方法
topic_type:
- apiref
api_name:
- IDebugAdvanced2.Request
- IDebugAdvanced3.Request
api_location:
- dbgeng.h
api_type:
- COM
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1da1e8f81ae3c68a458cfb04e3ac0e1f8824b501
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104066"
---
# <a name="idebugadvanced2request-method"></a>IDebugAdvanced2：： Request 方法


**请求**方法执行各种不同的操作。

<a name="syntax"></a>语法
------

```cpp
HRESULT Request(
  [in]            ULONG  Request,
  [in, optional]  PVOID  InBuffer,
  [in]            ULONG  InBufferSize,
  [out, optional] PVOID  OutBuffer,
  [in]            ULONG  OutBufferSize,
  [out, optional] PULONG OutSize
);
```

<a name="parameters"></a>参数
----------

*请求* \[中\]  
指定要执行的操作。 **请求** 可以是下表中的值之一。 可以通过使用 "请求" 列中的链接找到每个操作的详细信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">请求</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="debug-request-source-path-has-source-server.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SOURCE_PATH_HAS_SOURCE_SERVER&lt;/strong&gt;](debug-request-source-path-has-source-server.md)"><strong>DEBUG_REQUEST_SOURCE_PATH_HAS_SOURCE_SERVER</strong></a></p></td>
<td align="left"><p>检查源服务器的源路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-target-exception-context.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT&lt;/strong&gt;](debug-request-target-exception-context.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT</strong></a></p></td>
<td align="left"><p>返回用户模式小型转储文件中存储事件的 <a href="/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context" data-raw-source="[thread context](./scopes-and-symbol-groups.md#thread-context)">线程上下文</a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-exception-thread.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_THREAD&lt;/strong&gt;](debug-request-target-exception-thread.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_THREAD</strong></a></p></td>
<td align="left"><p>返回用户模式小型转储文件中存储事件的操作系统线程 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-target-exception-record.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_RECORD&lt;/strong&gt;](debug-request-target-exception-record.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_RECORD</strong></a></p></td>
<td align="left"><p>返回用户模式小型转储文件中存储事件的异常记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-get-additional-create-options.md)"><strong>DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>返回默认的进程创建选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-set-additional-create-options.md)"><strong>DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>设置默认的进程创建选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-win32-major-minor-versions.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS&lt;/strong&gt;](debug-request-get-win32-major-minor-versions.md)"><strong>DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS</strong></a></p></td>
<td align="left"><p>返回目标上当前正在运行的 Windows 的版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/previous-versions/ff541575(v=vs.85)" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM&lt;/strong&gt;](/previous-versions/ff541575(v=vs.85))"><strong>DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM</strong></a></p></td>
<td align="left"><p>从用户模式小型转储目标读取流。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-can-detach.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_CAN_DETACH&lt;/strong&gt;](debug-request-target-can-detach.md)"><strong>DEBUG_REQUEST_TARGET_CAN_DETACH</strong></a></p></td>
<td align="left"><p>检查以确定调试器引擎是否可以与当前进程分离 (使进程保持运行，但不再被调试) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-local-implicit-command-line.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE&lt;/strong&gt;](debug-request-set-local-implicit-command-line.md)"><strong>DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE</strong></a></p></td>
<td align="left"><p>设置 <a href="/windows-hardware/drivers/debugger/introduction#debugger-engine" data-raw-source="[debugger engine](./introduction.md#debugger-engine)">调试器引擎</a>的隐式命令行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-captured-event-code-offset.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET&lt;/strong&gt;](debug-request-get-captured-event-code-offset.md)"><strong>DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET</strong></a></p></td>
<td align="left"><p>返回当前事件的指令指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-read-captured-event-code-stream.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM&lt;/strong&gt;](debug-request-read-captured-event-code-stream.md)"><strong>DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM</strong></a></p></td>
<td align="left"><p>在当前事件的指令指针处最多返回64字节的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-ext-typed-data-ansi.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_EXT_TYPED_DATA_ANSI&lt;/strong&gt;](debug-request-ext-typed-data-ansi.md)"><strong>DEBUG_REQUEST_EXT_TYPED_DATA_ANSI</strong></a></p></td>
<td align="left"><p>执行多种不同的操作，有助于解释类型化数据。</p></td>
</tr>
</tbody>
</table>

 

*InBuffer* \[in，可选\]  
指定此方法的输入。 输入的类型和解释取决于 *请求* 参数。

*InBufferSize* \[中\]  
指定输入缓冲区 *InBuffer*的大小。 如果请求不需要输入，则应将 *InBufferSize* 设置为零。

*OutBuffer* \[out，可选\]  
接收此方法的输出。 输出的类型和解释取决于 *请求* 参数。 如果 *OutBuffer* 为 **NULL**，则不返回输出。

*OutBufferSize* \[中\]  
指定输出缓冲区 *OutBufferSize*的大小。 如果返回到 *OutBuffer* 的输出的类型具有已知大小，则 *OutBufferSize* 通常应为该大小，即使 *OutBuffer* 设置为 **NULL**也是如此。

*外部* \[out，可选\]  
接收在输出缓冲区 *OutBuffer*中返回的输出的大小。 如果 *外部* 为 **NULL**，则不返回此信息。

<a name="return-value"></a>返回值
------------

返回值的解释取决于 *Request* 参数的值。 除非另有说明，否则可能返回以下值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>S_OK</strong></td>
<td align="left"><p>方法成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S_FALSE</strong></td>
<td align="left"><p>方法成功。 但是，输出不适合输出缓冲区 <em>OutBuffer</em>，因此返回了截断的输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>E_INVALIDARG</strong></td>
<td align="left"><p>输入缓冲区的大小 <em>InBufferSize</em> 或输出缓冲区 <em>OutBufferSize</em> 的大小不是预期值。</p></td>
</tr>
</tbody>
</table>

 

此方法可能还会返回错误值。 有关更多详细信息，请参阅 [**返回值**](./hresult-values.md) 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Dbgeng (包含 Dbgeng) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**IDebugAdvanced2**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced2)

[**IDebugAdvanced3**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced3)

[**调试 \_ 请求 \_ 源 \_ 路径 \_ 包含 \_ 源 \_ 服务器**](debug-request-source-path-has-source-server.md)

[**调试 \_ 请求 \_ 目标 \_ 异常 \_ 上下文**](debug-request-target-exception-context.md)

[**调试 \_ 请求 \_ 目标 \_ 异常 \_ 线程**](debug-request-target-exception-thread.md)

[**调试 \_ 请求 \_ 目标 \_ 异常 \_ 记录**](debug-request-target-exception-record.md)

[**调试 \_ 请求 \_ 获取 \_ 其他 \_ 创建 \_ 选项**](debug-request-get-additional-create-options.md)

[**调试 \_ 请求 \_ 设置 \_ 附加 \_ 创建 \_ 选项**](debug-request-set-additional-create-options.md)

[**调试 \_ 请求 \_ 获取 \_ WIN32 \_ 主要 \_ 次要 \_ 版本**](debug-request-get-win32-major-minor-versions.md)

[**调试 \_ 请求 \_ 读取 \_ 用户 \_ 小型转储 \_ 流**](/previous-versions/ff541575(v=vs.85))

[**调试 \_ 请求 \_ 目标 \_ 可以 \_ 分离**](debug-request-target-can-detach.md)

[**调试 \_ 请求 \_ 集 \_ 本地 \_ 隐式 \_ 命令 \_ 行**](debug-request-set-local-implicit-command-line.md)

[**调试 \_ 请求 \_ 获取 \_ 捕获的 \_ 事件 \_ 代码 \_ 偏移量**](debug-request-get-captured-event-code-offset.md)

[**调试 \_ 请求 \_ 读取 \_ 捕获的 \_ 事件 \_ 代码 \_ 流**](debug-request-read-captured-event-code-stream.md)

