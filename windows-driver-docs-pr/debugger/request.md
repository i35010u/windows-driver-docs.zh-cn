---
title: IDebugAdvanced2 请求方法
description: 请求方法不会执行各种不同的操作。
ms.assetid: efb3c93c-5405-418b-a063-afa8e5e9e59a
keywords:
- 请求方法 Windows 调试
- 请求 Windows 调试，IDebugAdvanced2 接口的方法
- IDebugAdvanced2 接口 Windows 调试，请求方法
- 请求 Windows 调试，IDebugAdvanced3 接口的方法
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
ms.openlocfilehash: 523f1c29b974531d62984e36fc82e7db8544c2ab
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393111"
---
# <a name="idebugadvanced2request-method"></a>IDebugAdvanced2::Request 方法


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

<a name="parameters"></a>Parameters
----------

*请求*\[中\]  
指定要执行哪些操作。 **请求**可以是下表中的值之一。 可以按照"请求"列中的链接找到的每个操作的详细信息。

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
<td align="left"><p>返回<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context" data-raw-source="[thread context](https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context)">线程上下文</a>用户模式的小型转储文件中存储的事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-exception-thread.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_THREAD&lt;/strong&gt;](debug-request-target-exception-thread.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_THREAD</strong></a></p></td>
<td align="left"><p>返回在用户模式的小型转储文件中存储事件的操作系统线程 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-target-exception-record.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_RECORD&lt;/strong&gt;](debug-request-target-exception-record.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_RECORD</strong></a></p></td>
<td align="left"><p>返回在用户模式的小型转储文件中存储事件的异常记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-get-additional-create-options.md)"><strong>DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>返回的默认进程创建选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-set-additional-create-options.md)"><strong>DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>设置默认的过程创建选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-win32-major-minor-versions.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS&lt;/strong&gt;](debug-request-get-win32-major-minor-versions.md)"><strong>DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS</strong></a></p></td>
<td align="left"><p>返回在目标系统当前正在运行的 Windows 版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff541575(v=vs.85)" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))"><strong>DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM</strong></a></p></td>
<td align="left"><p>从用户模式的小型转储目标读取流。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-can-detach.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_CAN_DETACH&lt;/strong&gt;](debug-request-target-can-detach.md)"><strong>DEBUG_REQUEST_TARGET_CAN_DETACH</strong></a></p></td>
<td align="left"><p>检查是否可以为调试器引擎从当前进程 （离开进程正在运行但不能再调试） 分离。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-local-implicit-command-line.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE&lt;/strong&gt;](debug-request-set-local-implicit-command-line.md)"><strong>DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE</strong></a></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine" data-raw-source="[debugger engine](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)">调试器引擎</a>的隐式命令行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-captured-event-code-offset.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET&lt;/strong&gt;](debug-request-get-captured-event-code-offset.md)"><strong>DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET</strong></a></p></td>
<td align="left"><p>返回当前事件的指令指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-read-captured-event-code-stream.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM&lt;/strong&gt;](debug-request-read-captured-event-code-stream.md)"><strong>DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM</strong></a></p></td>
<td align="left"><p>返回最多 64 个字节的内存在当前事件的指令指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-ext-typed-data-ansi.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_EXT_TYPED_DATA_ANSI&lt;/strong&gt;](debug-request-ext-typed-data-ansi.md)"><strong>DEBUG_REQUEST_EXT_TYPED_DATA_ANSI</strong></a></p></td>
<td align="left"><p>中解释的类型化数据执行各种帮助的不同操作。</p></td>
</tr>
</tbody>
</table>

 

*InBuffer* \[in，可选\]  
指定此方法的输入。 类型和输入的解释取决于*请求*参数。

*InBufferSize* \[in\]  
指定的输入缓冲区的大小*InBuffer*。 如果该请求要求不需要输入*InBufferSize*应设置为零。

*OutBuffer* \[出时，可选\]  
接收来自此方法的输出。 类型和输出的解释取决于*请求*参数。 如果*OutBuffer*是**NULL**，则不返回输出。

*OutBufferSize* \[in\]  
指定的输出缓冲区的大小*OutBufferSize*。 如果输出的类型返回给*OutBuffer*具有已知的大小， *OutBufferSize*通常应正好为该大小，即使*OutBuffer*设置为**NULL**。

*外部*\[出时，可选\]  
接收输出缓冲区中返回的输出的大小*OutBuffer*。 如果*外部*是**NULL**，则不返回此信息。

<a name="return-value"></a>返回值
------------

返回值的解释取决于的值*请求*参数。 除非另行说明，否则可能会返回以下值。

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
<td align="left"><p>此方法已成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S_FALSE</strong></td>
<td align="left"><p>此方法已成功。 但是，在输出缓冲区中无法容纳输出<em>OutBuffer</em>，因此返回被截断的输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>E_INVALIDARG</strong></td>
<td align="left"><p>输入缓冲区的大小<em>InBufferSize</em>或输出缓冲区的大小<em>OutBufferSize</em>不是预期值。</p></td>
</tr>
</tbody>
</table>

 

此方法还可能返回错误值。 请参阅[**返回值**](https://docs.microsoft.com/windows-hardware/drivers/debugger/hresult-values)的更多详细信息。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Dbgeng.h （包括 Dbgeng.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**IDebugAdvanced2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced2)

[**IDebugAdvanced3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced3)

[**DEBUG\_REQUEST\_SOURCE\_PATH\_HAS\_SOURCE\_SERVER**](debug-request-source-path-has-source-server.md)

[**DEBUG\_REQUEST\_TARGET\_EXCEPTION\_CONTEXT**](debug-request-target-exception-context.md)

[**DEBUG\_REQUEST\_TARGET\_EXCEPTION\_THREAD**](debug-request-target-exception-thread.md)

[**DEBUG\_REQUEST\_TARGET\_EXCEPTION\_RECORD**](debug-request-target-exception-record.md)

[**DEBUG\_REQUEST\_GET\_ADDITIONAL\_CREATE\_OPTIONS**](debug-request-get-additional-create-options.md)

[**DEBUG\_REQUEST\_SET\_ADDITIONAL\_CREATE\_OPTIONS**](debug-request-set-additional-create-options.md)

[**调试\_请求\_获取\_WIN32\_主要\_次要\_版本**](debug-request-get-win32-major-minor-versions.md)

[**DEBUG\_REQUEST\_READ\_USER\_MINIDUMP\_STREAM**](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))

[**DEBUG\_REQUEST\_TARGET\_CAN\_DETACH**](debug-request-target-can-detach.md)

[**DEBUG\_REQUEST\_SET\_LOCAL\_IMPLICIT\_COMMAND\_LINE**](debug-request-set-local-implicit-command-line.md)

[**调试\_请求\_获取\_CAPTURED\_事件\_代码\_偏移量**](debug-request-get-captured-event-code-offset.md)

[**调试\_请求\_读取\_CAPTURED\_事件\_代码\_流**](debug-request-read-captured-event-code-stream.md)

 

 






